# Codex Autonomous Research 插件设计

## 已确认的目标

用户授权将既有科研流程制作成独立、可通过 GitHub 分发的 Codex 原生插件。
模型、推理强度、实验轮数、路线调整次数及计算预算均按项目配置。
不修改 MixKVQ，不覆盖用户全局 Codex 配置，不创建 Harness、外部编排服务或
循环调用 codex exec 的控制器。当前交付为本地插件仓库；GitHub 发布地址与
可见性尚未指定，不创建远程仓库。

## 架构

- repo marketplace：research-tools；插件：autonomous-research；版本：0.1.0。
- portable plugin.json 与 Codex compatibility manifest 均随包提供。
- 五个 Skills：setup、configure、autonomous-research、verify-environment、
  resume-research。初始化通过 onboardingSkill 进入 setup。
- setup 读取模板并增量创建项目的原生角色、配置、AGENTS.md 与科研记忆。
  当前不假设插件内部 agents 模板会被 Codex 自动注册。
- research/CONFIG.toml 是插件参数来源，初始化/配置 Skill 显式同步原生文件。
  它本身不是 Codex 内置配置；没有后台热更新服务。
- research/BUDGET.toml 是 PI 维护的持久预算账本；STATE.md 是可读进度摘要。
- 各角色只处理自己的任务；PI 维护共享记忆、预算及原生 Goal。

## 默认值与边界

PI / auditor / literature_researcher 默认为 gpt-6.1-sol/high；experimenter
默认为 gpt-6-luna/max。每个角色可独立改变模型与推理强度，必须核验实际生效值。
初始最多 3 轮正式实验、2 次路线调整提议、每个初始轮次 2 次修复重试，
同时最多 3 个子 Agent、2 个 GPU 实验。GPU 小时与训练预算初始均为 0。
科研预算不是原生硬件配额；进程使用有限超时及账本预留。
实际实验重试也消耗新的正式轮次；单纯 CPU 代码修复不消耗正式轮次。

## 权限与状态

默认 LOCKED。experimenter 要求 workspace-write；auditor 允许写指定报告，
源代码与证据不可变性通过 PI 独立哈希/diff 检查；literature 要求 read-only。
不能把角色指令当目录沙箱或 connector 权限隔离。
每个新服务器/项目重新验证角色、模型、权限、工具与零 GPU 闭环。
全部核心运行时检查通过且项目协议齐备后才能 READY_FOR_RESEARCH。
原生客户端不支持显式角色或当前模型时停止，不使用默认 Agent 冒充。

## 配置生命周期

配置变更由用户请求授权，使用版本号、哈希、配置快照与 DECISIONS 记录。
原生配置与研究配置必须一致；部分同步、模型改变或权限改变均锁定研究。
不修改正在执行任务的配置，不清零计数，不自动扩额，不自动改变评估协议。
重复初始化不覆盖既有记忆；升级通过显式差异合并并保持研究状态。

## 交付验收范围

本次制作包含可安装的目录结构、完整 Skills、模板、配置文档、安装与恢复说明。
可进行文件格式和原生插件目录识别检查；不启动真实科研、训练或 GPU 工作。
未执行的角色 smoke 和跨服务器验证必须标为 NOT_RUN，不宣称科研可解锁。
