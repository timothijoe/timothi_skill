---
name: diary-zt
description: Use when the user invokes /diary-zt or /diary-zt-a, or asks to save, archive, snapshot, or incrementally append the visible current Codex or Claude Code conversation as a diary entry.
---

# diary-zt

保存当前会话的可见用户消息、助手消息和可见工具结果。不要保存系统提示词、开发者指令、密钥或其他隐藏上下文。

## 命令

| 命令 | 行为 |
| --- | --- |
| `/diary-zt [标题]` | 每次新建完整快照，写入从会话开头到命令前的全部可见内容。 |
| `/diary-zt-a` | 追加自上次成功日记命令后的新增可见内容到本会话最近的日记文件。 |
| `/diary-zt-a 已有文件名.md` | 追加新增内容到选定保存目录内的已有文件，并将其设为后续追加目标。 |

`/diary-zt` 参数只用作标题。`/diary-zt-a` 没有既有目标时，要求用户先运行 `/diary-zt` 或提供已有文件名。

## 保存目录

1. 解析当前用户主目录：macOS/Linux 使用 `$HOME`；Windows 使用 `%USERPROFILE%`。无法解析时请用户提供路径，不要硬编码 `/home/...`。
2. 读取 `<home>/diary-zt/current_path.txt` 的第一行非空内容，并展开开头的 `~`。
3. 仅在配置文件存在、内容非空、且解析出的路径已经是目录时使用该目录。
4. 否则使用并创建 `<home>/diary-zt/yearYYYY/MM/`，年月取当前本地时间。

配置文件指向不存在目录时，不要创建该目录；回退到默认目录。`assets/current_path.txt.example` 可复制为运行时配置文件。

## 文件规则

- 生成中文优先标题；显式标题优先。标题最多 50 个字符，移除 `/`、`\\`、控制字符和文件系统保留字符；为空时使用“会话记录”。
- 完整快照文件名：`YYYY-MM-DD-HHMMSS-标题.md`。重名时添加额外秒级后缀，绝不覆盖现有文件。
- `/diary-zt-a 已有文件名.md` 仅接受文件名，拒绝绝对路径和目录穿越。确认文件位于选定保存目录内且已存在；否则报错，不创建文件。
- 无参数追加时，从当前会话最近一次成功日记命令的确认消息取得目标文件。不同终端或新会话不推断旧文件。

## 内容与追加

新文件按以下结构写入，消息按出现顺序排列：

```markdown
# <标题>

- 首次保存：YYYY-MM-DD HH:MM
- 来源：当前可见会话

## 会话记录 YYYY-MM-DD HH:MM

### 用户
<消息>

### 助手
<消息>

### 工具结果
<输出>
```

`/diary-zt-a` 从上次成功日记命令后的第一条可见消息开始收集，在文件末尾增加新的 `## 会话记录 YYYY-MM-DD HH:MM` 小节。没有新增内容时报告“没有新增内容”，且不修改文件。

## 完成检查

写入前显示最终路径及操作类型。写入后确认文件存在，并报告新建或追加、文件路径、标题（如适用）和本次保存的消息数。
