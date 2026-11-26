# ReasearchToolworkspace
for Xueyuqin do reasearch

## 工具索引

| 工具 | 用途 | 说明 |
| --- | --- | --- |
| `survey-workbench` | 整理文献、生成调研报告与科研汇报 PPT | [中文说明](tools/survey-workbench/README.md) · [English](tools/survey-workbench/README_EN.md) |

## 工作区管理

- 每个工具放在 `tools/<工具名>/`，保留自身的说明、脚本、模板和资源，并在上面的索引登记。
- 本地调研资料、生成的报告和其他运行产物统一存放在根目录的 `runs/<课题名>/`，该目录由 Git 忽略。
- 实际凭据放在本地 `.env`。仓库可以保留 `.env.example` 作为配置样例。
