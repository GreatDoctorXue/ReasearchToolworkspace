# ReasearchToolworkspace
for Xueyuqin do reasearch

## 交给 AI 使用

已有 Harness / Loop 的 Agent（如 Codex、Claude Code、Gemini CLI）使用自身的执行循环与任务管理，从 [AGENTS.md](AGENTS.md) 和 [工具目录](tools/README.md) 进入。可以直接发送下面这句话。

```text
请读取仓库根目录的 AGENTS.md 和 tools/README.md，按需加载工具说明。
使用你自身的 Harness / Loop。我的任务是「填写你的研究主题和目标」。
```

需要仓库提供执行流程时，再选择 [可选 Harness 指南](harness/README.md)，其中包含循环、任务记录与续跑约定。
Codex、Claude Code、Gemini CLI 分别有对应的仓库入口文件。其他平台可显式读取或上传上述文档。
执行脚本需要平台提供文件读写、Python 和相应网络能力。

## 工具索引

| 工具 | 用途 | 说明 |
| --- | --- | --- |
| `survey-workbench` | 整理文献、生成调研报告与科研汇报 PPT | [使用与验收](tools/survey-workbench/USAGE.md) · [中文说明](tools/survey-workbench/README.md) · [English](tools/survey-workbench/README_EN.md) |

## 工作区管理

- 每个工具放在 `tools/<工具名>/`，保留自身的说明、脚本、模板和资源，并在上面的索引登记。
- 本地调研资料、生成的报告和其他运行产物统一存放在根目录的 `runs/<课题名>/`，该目录由 Git 忽略。
- 实际凭据放在本地 `.env`。仓库可以保留 `.env.example` 作为配置样例。
