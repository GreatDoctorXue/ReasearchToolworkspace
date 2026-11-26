# survey-workbench 操作指南

用于文献检索、资料归档、资料库查询、调研报告和基于报告的 PPT。按本次已确认的任务读取 [工具规则](SKILL.md) 的相应章节，操作分类见下方“按目标选择步骤”。
工具规则中的 P0–P9 描述调研业务步骤，由宿主 Agent 调度执行。
以下 Bash 命令从仓库根目录运行，Windows 环境使用对应的路径和虚拟环境解释器。

## 路径与环境

需要脚本处理或保存课题材料时设置路径，将 `survey_topic` 换为课题名。恢复任务时将 `RUN` 指向已有任务目录。

```bash
REPO_ROOT="$(pwd)"
SCRIPTS="$REPO_ROOT/tools/survey-workbench/scripts"
RUN="$REPO_ROOT/runs/survey_topic"
mkdir -p "$RUN"
```

完整建库、解析和报告导出使用 Python 3.9+ 及下列依赖。执行单项功能时，复用现有环境并检查该功能实际需要的依赖。首次完整配置可在仓库虚拟环境安装。

```bash
python3 -m venv "$REPO_ROOT/.venv"
PY="$REPO_ROOT/.venv/bin/python"
"$PY" -m pip install openpyxl pymupdf pdfplumber python-docx beautifulsoup4
```

已有虚拟环境时直接设置 `PY`。运行环境检查会请求多个数据源和本地 Zotero，实际耗时取决于网络超时。

```bash
"$PY" "$SCRIPTS/check_env.py" --json > "$RUN/env.json"
```

读取 JSON 中的 `python_ok`、`ready`、`packages` 和 `usable_sources`，确认版本、依赖与可用数据源。
检查命令退出成功后仍需检查这些字段。无可用数据源时可继续处理本地资料，并记录检索缺口。

## 按目标选择步骤

| 目标 | 执行范围与输入 |
| --- | --- |
| 新建文献与资料库 | 按 SKILL 的 P1–P6 执行，筛选后再获取资料 |
| 查询或打标已有库 | 先检查 `00_索引/library.db`，按 P7 执行 |
| 编写调研报告 | 从现有库与解析全文进入 P8，读取 `references/report-spec.md` |
| 生成汇报 PPT | 从现有报告进入 P9，读取内置 PPT 引擎与交接指南 |

检索命令示例，替换中英文主题，并根据 `usable_sources` 设置 `--sources`。

```bash
"$PY" "$SCRIPTS/search_all.py" "composite curing optimization" \
  --query-zh "复合材料固化工艺优化" --kind paper --limit 40 --root "$RUN"
```

读取 `$RUN/.cache/search_raw/merged.json` 并按 P3 筛选，再按 P4–P6 获取、归档、解析和建索引。
运行 `acquire.py` 时如需提供联系邮箱，使用用户确认的邮箱。参数不清楚时对相应脚本运行 `--help`。

已有资料库可直接查询。

```bash
"$PY" "$SCRIPTS/query.py" stats --root "$RUN"
"$PY" "$SCRIPTS/query.py" list -n 20 --root "$RUN"
```

新建报告时生成骨架，随后由模型依据真实来源撰写正文。续写已有报告时先读取已有成稿。

```bash
"$PY" "$SCRIPTS/make_report.py" --root "$RUN" --topic "复合材料固化工艺优化"
```

PPT 先运行下列命令生成交接材料，再执行 [PPT 引擎规则](ppt_skill/SKILL.md) 和 [调研库交接约定](ppt_skill/SURVEY_INTEGRATION.md)。

```bash
"$PY" "$SCRIPTS/ppt_handoff.py" --root "$RUN"
```

`ppt_handoff.py` 产出 `05_报告/ppt_source/source.md`。最终 PPT 的生成与 QA 仍需按引擎流程执行。
PPT 依赖和可选图像后端按引擎说明安装或配置。

## 验收与交付

| 产物 | 真实位置与验收方式 |
| --- | --- |
| 文献与资料库 | 检查 `01_文献/`、`02_开放资料/` 和实际获取状态，查询统计并抽查原文件 |
| 索引 | 打开 `00_索引/索引表.xlsx`，确认 `00_索引/library.db` 可查询，核对记录与来源 |
| 报告 | 对实际成稿运行下方检查，核实引文和页码，再导出并打开 DOCX |
| PPT | 检查交接材料，按引擎 QA 检查生成的 PPTX 及渲染结果 |
| 资料缺口 | 检查 `05_报告/未获取资料清单.md` 与实际失败记录，说明待处理项 |

报告校验和导出示例，将文件名替换为实际成稿路径。

```bash
"$PY" "$SCRIPTS/make_report.py" --root "$RUN" \
  --check "$RUN/05_报告/研究现状_复合材料固化工艺优化.md"
"$PY" "$SCRIPTS/export_docx.py" --root "$RUN" \
  "$RUN/05_报告/研究现状_复合材料固化工艺优化.md"
```

校验返回 `PASS` 后执行导出。按宿主 Agent 的方式记录执行结果，告知用户实际产物路径、已完成的验证与资料缺口。
