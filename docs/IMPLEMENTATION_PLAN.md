# Codex Autonomous Research Implementation Plan

**Goal:** 制作独立、可配置的 Codex 原生科研插件。
**Architecture:** Skills 驱动项目增量初始化与科研闭环，Custom Agents 执行角色任务，
Goal Mode 维持目标；模板与项目科研状态分开存储。
**Tech Stack:** Markdown / TOML / JSON，Codex 原生插件与 Git。
**Spec:** [DESIGN.md](DESIGN.md)。
**Execution:** 当前会话由 PI 直接实现，用户已授权制作上述插件。

## 约束

- 不修改既有项目与全局 Codex 配置。
- 不实现运行时控制器；不自动发布或启动科学实验。
- 不添加测试程序或调用科研模型。检查文件格式不能替代角色运行时验证。

## 实现任务

- [x] 创建原生 marketplace、portable/compatibility manifests 与独立 Git 仓库。
- [x] 创建角色、项目配置、协议、科研记忆与预算模板。
- [x] 编写初始化、配置修改、科研闭环、环境验证与恢复 Skills。
- [x] 编写参数说明、安装指南、已知限制与发布说明。
- [x] 检查 JSON/TOML、路径引用和原生插件可识别性，保存实际证据。
- [x] 交付本地版本与归档；明确未运行的角色验证和未发布状态。

## 检查重点

已有配置冲突时保持原文件；缺少模型能力时保持 LOCKED；失败重试不返还预算；
模型变更不重置已用次数；插件升级不覆盖科研记忆或已锁定协议；父会话权限
继承不能被报告为独立角色隔离；模板中的 UNSET 是阻塞状态，不是真实研究结论。
