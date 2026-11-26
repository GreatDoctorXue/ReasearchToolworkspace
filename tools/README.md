# 工具目录

本页提供工具发现入口。按用户目标读取所选工具的使用指南和 `SKILL.md`，再调用相应脚本。
执行循环、重试和任务状态采用宿主 Agent 已有机制。工具使用指南说明依赖、输入、命令、产物与验收方式。

| 工具 | 适用任务 | 使用与验收 | 完整规则 |
| --- | --- | --- | --- |
| survey-workbench | 文献检索与资料库、查询打标、调研报告、科研汇报 PPT | [USAGE.md](survey-workbench/USAGE.md) | [SKILL.md](survey-workbench/SKILL.md) |

## 接入新工具

1. 将工具放在 `tools/<工具名>/`，提供 README、`SKILL.md` 或等效操作说明。
2. 在工具目录的 `USAGE.md` 中写明适用任务、依赖、真实入口命令、输出位置与验收命令。
3. 在本页、根 README 和 `AGENTS.md` 的工具表中添加入口。
4. 验证文档链接和示例命令，并记录验证范围。
