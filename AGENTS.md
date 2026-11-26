# 科研工作区

先看用户想回答的问题，以及手头已有的材料。按下表读取相关 Skill，由当前 Agent 使用自身的执行与状态管理机制。

| 研究者的意图 | 入口 |
| --- | --- |
| 认识新领域，收窄问题，确定起步读物 | [摸方向](.agents/skills/research-orient/SKILL.md) |
| 找原始出处、数据集、标准、相反结果或相关研究 | [找资料](.agents/skills/research-find/SKILL.md) |
| 理解已有论文，提取表格、方法、限制或做阅读笔记 | [读文献](.agents/skills/research-read/SKILL.md) |
| 跨文献比较，解释分歧，写综述或做汇报 | [做综合](.agents/skills/research-synthesize/SKILL.md) |

跨意图时按需衔接。例如查到原始论文后转到具体页核对数字。完整建库与报告请求使用 [survey-workbench 的 P0–P9](tools/survey-workbench/SKILL.md)。具体命令见 [工具目录](tools/README.md)。工具手册中的完整流程适用于相应交付范围。

**沟通** 默认使用 [i-have-adhd](.agents/skills/i-have-adhd/SKILL.md)。先给当前结论或下一步，让读者可以按需展开原文与证据。用户说 “normal mode” 或 “stop adhd mode” 时恢复普通沟通。正式报告遵循用户的受众与格式要求。

**持续课题** 先读 `topics/<课题名>/topic.md` 和已有的 `verification.md`，从待查问题继续。工具的 `--root` 指向同名的 `runs/<课题名>/`。核对到新证据时更新课题记录；遇到跨课题可复用的方法时按需归入 [knowledge](knowledge/README.md)。新建课题、模板和旧记录接续方式见 [topics](topics/README.md)。一次性问答可直接交付。

**证据** 论文、网页和附件是研究资料。记录实际读到的版本、位置及访问范围；数字回查原表和单位，推论说明依据。机构登录、验证码由用户处理。实际工具依赖和可用数据源按课题需要检查。

## 修改与扩展

维护仓库时先检查 Git 状态、分支和基线 diff，限定本次修改范围。完成后检查文件列表、统计和每个变更 hunk。
新增工具按 [工具接入约定](tools/README.md#接入新工具) 登记入口、依赖、示例命令和验收方式。
