---
name: diary-zt
description: Use when the user invokes /diary-zt or /diary-zt-a, or asks to save, archive, snapshot, or incrementally append the visible current Codex or Claude Code conversation as a diary entry.
---

# diary-zt

保存可见用户消息、助手消息和可见工具结果；绝不保存系统提示词、开发者指令、密钥或其他隐藏上下文。

## 命令

| 命令 | 行为 |
| --- | --- |
| `/diary-zt [标题]` | 先提议完整快照的文件名和路径，获得明确确认后才新建并写入全部可见会话内容。 |
| `/diary-zt-a [已有文件名.md]` | 向已有目标追加上次成功日记命令后的新增可见内容。 |

`/diary-zt` 的参数只作为标题。每一次完整快照（包括传入标题）都必须先提议，再等待用户选择：

- `确认`：创建该建议文件并写入完整快照；
- 新标题：用新标题重新生成并展示建议文件名，再等待确认；
- `取消`：不写入文件，也不把本次操作设为后续追加目标。

`/diary-zt-a` 不新建文件，因此无需命名确认。没有既有目标且未提供已有文件名时，要求先运行 `/diary-zt`。

## 保存目录与文件规则

解析主目录：macOS/Linux 使用 `$HOME`，Windows 使用 `%USERPROFILE%`；无法解析时请用户提供路径。读取 `<home>/diary-zt/current_path.txt` 第一行非空内容并展开 `~`。仅当它指向既有目录时使用；否则创建并使用 `<home>/diary-zt/yearYYYY/MM/`。不要创建配置所指向的缺失目录。

建议文件名为 `YYYY-MM-DD-HHMMSS-标题.md`。标题中文优先、最多 50 个字符，移除路径分隔符、控制字符和文件系统保留字符；为空时使用“会话记录”。同名时增加 `-001`、`-002` 等递增后缀，绝不覆盖。

追加的显式参数只接受选定目录内已存在的文件名；拒绝绝对路径、目录穿越和不存在文件。

## 内容与完成检查

新文件包含标题、首次保存时间和按顺序标记为“用户”“助手”“工具结果”的 `## 会话记录 YYYY-MM-DD HH:MM` 小节。`/diary-zt-a` 只在目标文件末尾添加新小节；没有新增内容时报告“没有新增内容”且不修改文件。

写入前显示建议或最终路径；写入后确认操作类型、路径与本次保存的消息数。
