# Codex Autonomous Research

将科学研究流程作为 Codex 原生插件安装到不同服务器，并用于不同科研项目。
模型、推理强度、实验轮数、路线调整次数和计算预算可按项目配置。

版本：**0.1.0**。分发目录：`research-tools`；插件：`autonomous-research`。
此仓库仅包含 Skills、角色/配置模板和文档，没有 Harness、Agent 服务或循环
调用 codex exec 的控制器。安装不自动运行实验。

## 安装

服务器需有支持插件、Custom Agents 和 Goal Mode 的原生 Codex 客户端。
账号须能使用选定模型；具体客户端、特性、权限在目标项目重新验证。

### 本地安装

在任意目录执行，路径替换为此仓库的实际位置：

```bash
codex plugin marketplace add /absolute/path/to/codex-autonomous-research
codex plugin add autonomous-research@research-tools
```

这两条命令由你执行时会登记/安装插件；制作本地插件不会代替你修改全局配置。
安装后重启 Codex。多个同名 marketplace 如有冲突，先检查 native marketplace
list，明确要采用的源，不自动移除其他来源。

### 从 GitHub 安装

发布到自己的仓库并创建版本标签后：

```bash
codex plugin marketplace add OWNER/codex-autonomous-research --ref v0.1.0
codex plugin add autonomous-research@research-tools
```

`OWNER` 是待发布时替换的用户名；这不是已经存在的远程仓库。
无需进入官方公共插件目录即可使用自己的 Git marketplace。
使用私有仓库时，目标服务器需自行配置 Git 访问权限；不复制 Codex 登录凭据。

## 在科研项目中使用

进入目标项目，在 Codex 中按顺序发出：

1. **初始化：**“使用 autonomous-research 插件的 setup Skill 初始化当前科研项目，
   检查已有配置并增量合并，保留实验代码、记录和全局配置。”
2. **配置：**“使用 configure Skill：实验执行者用 gpt-6-luna/max，其他角色用
   gpt-6.1-sol/high；最多 5 轮实验、3 次路线调整。GPU 预算暂为 0。”
3. **重新开启可信的原生项目会话**，使角色及 PI 模型配置生效。
4. **验证：**“使用 verify-environment Skill，运行零 GPU 角色与虚拟科研闭环验证，
   用运行时元数据检查模型、推理强度和权限。失败时保持 LOCKED。”
5. **定义真实协议：**明确研究问题、成功标准、数据/输入、主指标、种子、基线、
   统计方法与训练/计算预算，记录用户授权。通过全部核心门槛后才能解锁。

初始化会生成项目原生 `.codex/agents/` 和配置、AGENTS.md 托管片段、项目科研
Skill、`research/CONFIG.toml`、预算账本、五份科研记忆及配置历史。
它不会假设插件模板中的角色会被原生客户端自动发现。

## 模型与预算

初始化/修改配置时读取 [CONFIG 模板](plugins/autonomous-research/templates/research/CONFIG.toml)。

| 参数 | 默认值 |
| --- | --- |
| PI / auditor / literature 模型 | gpt-6.1-sol / high |
| experimenter 模型 | gpt-6-luna / max |
| 正式实验轮数 | 3 |
| 路线调整提议次数 | 2 |
| 每个初始轮次的修复重试上限 | 2 |
| 同时活动子 Agent | 3，不含 PI |
| 同时 GPU 实验 | 2 |
| 单次实验时限 | 1800 秒 |
| 累计 GPU 小时 | 0，需明确授权才能增加 |
| 累计训练 updates / tokens | 0 / 0 |

模型 ID 和推理强度均可配置，但必须受账号/客户端支持。不会默默替换模型。
`research/CONFIG.toml` 是本插件的参数文件；configure Skill 将相应值增量同步
到原生配置，文件编辑本身没有后台热更新效果。

正式实验失败和实验重跑均消耗轮数与资源；重跑还受修复次数上限限制。
代码修复未运行正式实验时不消耗轮数。路线提议即使被拒绝也计数。
增加上限不重置已用次数；研究中变更留下配置版本、哈希和授权记录。
GPU 并发与 Agent 并发分别计数，属于 PI 账本和进程管理约束，不是原生硬件配额。
完整规则见 [配置契约](plugins/autonomous-research/references/configuration.md)。

## 科研闭环

PI 建立可证伪假设 → 最低成本实验 → experimenter 提交真实证据 → 新 auditor
独立审计 → 区分实现错误、证据不足和充分否证 → 必要时核实文献 → PI 提出
新机制并登记下一轮。不会把一次负结果判定为整个研究方向失败。

auditor 可写自己的报告；它不得修改被审计代码或证据。PI 独立检查哈希/diff。
这不是硬性目录写隔离。literature 默认要求实际 read-only；原生子会话继承父
权限可能使该要求失效，必须验证，失败时不能解锁。

## 使用 Goal Mode 与恢复

项目全部门槛通过后，在支持 Goal Mode 的原生客户端中输入：

```text
/goal 按当前项目已锁定协议与 research/CONFIG.toml 的预算，执行自主科研闭环，
直到达到 research/GOAL.md 的成功标准或需要我的明确授权。
```

达到研究预算后停止实验并请求授权；Goal Mode 不会取消项目预算。
暂停/恢复目标使用当前客户端提供的 `/goal pause`、`/goal resume` 等控制。
断线后优先用 `codex resume <PI-thread-id>` 恢复同一原生会话，再要求
resume-research Skill 核对进程、检查点、证据和预算。新会话从项目记忆恢复工作，
但不会自动继承旧会话的 Goal；需要时由用户重新启动 `/goal`。

## 升级、限制与发布

插件升级与项目配置迁移分开处理；setup 比较托管文件哈希，保留本地修改、
科研记忆、实验结果和预算。重装不得清零。

- [已知限制与兼容性](docs/COMPATIBILITY.md)
- [GitHub 发布说明](docs/PUBLISHING.md)
- [制作检查记录](docs/BUILD_REPORT.md)
- [设计](docs/DESIGN.md)

## 官方依据

- [插件格式、初始化和 Git marketplace](https://developers.openai.com/plugins/build/plugins)
- [Custom Agents 与模型配置](https://learn.chatgpt.com/docs/agent-configuration/subagents)
- [原生 Goal Mode](https://developers.openai.com/cookbook/examples/codex/using_goals_in_codex)
