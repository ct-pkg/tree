applies-to: v0.0.0

# v0-PH-0：仓库骨架与治理落地

| 项 | 值 |
| --- | --- |
| 编号 | `v0-PH-0` |
| 目标 | 建包骨架：`ct.pkg`、README、规范生成块与全文副本、决策与卡片目录、门禁入口 |
| 规范版本 | 1.17.0 |
| version-minor | 0（收口 `0.0.0`） |
| 依赖 | 无 |
| 状态 | 进行中（2026-11-22 起） |

## 范围

**做**：包清单与目录、`AGENTS.md` 生成块 + 实例化节、`docs/spec` 全文副本、D-001、两张卡片、
路线图与编号账本、session map、snippets 与 issue 台账占位。

**不做**：不写任何树容器实现；不建格式包；不发布 tag。

## 任务清单

| id | deliverable | verify | effort |
| --- | --- | --- | --- |
| T1 | `ct.pkg` + README + 目录骨架 | `ct pkg check .` | S |
| T2 | `AGENTS.md` 生成块与 `docs/spec` 全文副本 | `bash <规范来源>/bin/sync-agents.sh --check AGENTS.md` | S |
| T3 | 门禁入口：复制 ct/std 的 `tools/check.sh` + `tools/gate_checks.py`，改根路径与本仓特例；负例随脚本同拷并当天接红 | `bash tools/check.sh all` 绿 + 「故意弄坏必须红」自检 | M |
| T4 | 决策、卡片、路线图、编号账本、session map | `ls docs/decisions/D-001-tree-scope.md docs/phases/v0-PH-0/card.md docs/phases/v0-PH-1/card.md docs/planning/roadmap.md docs/session-map.md` 全部存在 | S |

## 进度

| 任务 | 状态 | 证据 |
| --- | --- | --- |
| T1 | done | `ct pkg check .` → `ok: 4 criteria` |
| T2 | done | `sync-agents.sh --check` 通过 |
| T3 | todo | 待 DEV 接入 |
| T4 | done | 本卡与 D-001 所在提交 |

## T3 细则

1. **fork 登记**：脚本复制自 `ct/std`，分叉走 `AGENTS.md` 0.3 的 deviation；同步触发为可判定形式——**源仓该脚本文件 `git diff` 非空即同步**，不写「择机」。
2. **公共化触发**：**第三个仓需要门禁脚本时**立项抽取公共实现（两个是巧合，三个是模式），抽取后删除本仓副本。
3. **负例同拷**：每条门禁的负例自测随脚本一起复制（「改一个状态即红」类），并在本仓 CI 立刻跑通「故意弄坏必须红」自检；负例未接红即 T3 未完成。

## 退出判据

- [x] `ct pkg check .` 通过。
- [x] `sync-agents.sh --check AGENTS.md` 通过。
- [ ] `bash tools/check.sh all` 退出码 0（T3 完成后）。
- [x] **任务清单每项可独立验收（6.6 T-6）**：上表逐项给 verify 命令。
