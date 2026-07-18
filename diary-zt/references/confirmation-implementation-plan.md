# diary-zt 命名确认实施计划

**Goal:** 让 `/diary-zt` 在写入完整会话快照前先提议文件名并等待用户确认。

## 修改文件

- `SKILL.md`：为完整快照增加提议、确认、改名与取消状态；保留 `/diary-zt-a` 直接追加行为。
- `references/design.md`：说明完整快照是两步流程。
- `references/testing.md`：增加确认、改名、取消和显式标题确认测试。

## 验证

1. 先检查现有 `SKILL.md` 不包含“等待确认”条款，作为基线。
2. 写入最小规则：每次 `/diary-zt` 均先显示建议路径；仅在明确确认后创建文件；新标题重新提议；取消不写入也不更新追加目标。
3. 检查 `SKILL.md`、设计和测试说明都包含确认流程。
4. 运行 `quick_validate.py diary-zt` 与 `git diff --check`。
