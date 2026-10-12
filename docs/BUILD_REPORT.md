# Plugin build report

日期：2026-10-12。插件版本：0.1.0。执行客户端：Codex CLI 0.162.1。

## 已完成

- 独立插件源目录与本地 Git 仓库；没有在 MixKVQ 内制作插件。
- 原生 marketplace、portable/compatibility manifests 和 onboarding setup。
- 五个 Skills、三个角色模板、可配置模型/推理强度与有限预算。
- 增量初始化、配置版本、预算账本、独立审计、恢复与迁移规则。
- 项目协议、五份科研记忆和明确 SIMULATED 的零 GPU 记录模板。
- 安装、使用 /goal、恢复任务、兼容性和 GitHub 发布文档。

本地源码使用 Codex 自动提交身份（Codex / codex@localhost），只为本次 Git
命令提供身份，不更改用户 Git 配置。交付归档来自本地提交，不含 .git 与 dist。

## 实际检查与证据

1. JSON/TOML 均通过标准库解析，包含两个插件 manifests、marketplace、角色和
   预算配置。Skill frontmatter 为 name/description，资源引用检查无缺失项。
   检查快照见 [package-check.json](evidence/package-check.json)。
2. 原生 CLI 通过仅本次命令的 marketplaces 参数识别目录：

   ```bash
   codex -c 'marketplaces.research-tools={source_type="local",source="<PACKAGE_ROOT>"}' \
     plugin list --available --marketplace research-tools --json
   ```

   返回 exit 0，available 中包含 autonomous-research@research-tools，version=0.1.0。
   installed=false，enabled=false。返回摘录见
   [native-catalog.json](evidence/native-catalog.json)，仅目录路径做通用化替换。
   在未登记 marketplace 的条件下，单纯当前目录 list 没有发现本目录；因此安装
   指南明确要求 native marketplace add，不依赖自动发现。
3. 用户全局 Codex config 哈希与制作前一致；MixKVQ tracked Git diff 为空。
   制作过程没有写入该项目的代码、配置或记忆。未启动 GPU/训练/推理/编译任务。

## 未执行或尚未确定

| 项目 | 状态 |
| --- | --- |
| 安装到用户全局 Codex | NOT_RUN；本次仅命令范围目录识别 |
| 新插件在项目中的 setup/configure 实际执行 | NOT_RUN |
| 新角色实际模型/effort/权限 smoke | NOT_RUN |
| 跨服务器运行验证 | NOT_RUN |
| GitHub 远程仓库创建 / push | NOT_RUN；未指定目标地址和可见性 |
| 开源许可证选择 | 未指定；本次没有替用户授予许可证 |

模板指定模型不能证明实际使用模型。以前 MixKVQ 的 runtime 日志不作为此插件的
新验证结果。文献角色只读可能被父权限覆盖的已知问题仍由目标项目验证并阻塞解锁。
本交付完成插件制作与目录识别，不声明任何科研项目 READY_FOR_RESEARCH。

## GPU 和科研预算

本次 GPU-hours=0，训练=0，真实实验轮次=0，真实路线调整=0。
打包、配置和虚拟记录模板不是科学实验结果。
