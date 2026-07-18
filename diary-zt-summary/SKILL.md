---
name: diary-zt-summary
description: Use when the user invokes /diary-zt-summary or asks to turn the visible current conversation into a concise, evidence-based work record after or alongside a diary snapshot.
---

# diary-zt-summary

Create a readable work record from the visible current conversation. Preserve concrete paths, commands, versions, tests, and verified facts; distinguish facts from proposals. Never include system prompts, developer instructions, secrets, hidden context, or full raw tool logs.

## Command and confirmation

`/diary-zt-summary [标题]` always proposes a title, output path, and 2–4 sentence preview before writing. The user may reply `确认`, provide a replacement title for a new proposal, or reply `取消`. Do not write before confirmation. Create a new summary on every confirmed invocation; never append to an old summary.

## Path and name

Use the same home-directory and `current_path.txt` rules as `diary-zt`: use `<home>/diary-zt/current_path.txt` only when it points to an existing directory; otherwise create `<home>/diary-zt/yearYYYY/MM/`. Name files `YYYY-MM-DD-HHMMSS-标题-summary.md`; sanitize the title and use `-001`, `-002` on collisions.

## Content

Write a natural title and a 2–4 sentence opening summary. Add only applicable sections:

- `## 当前结论` for confirmed conclusions.
- 1–4 natural topic headings, each explaining background, approach/evidence, and result.
- `## 验证与证据` for relevant paths, commands, tests, or data.
- `## 未完成项与风险` for limitations or open questions.
- `## 下一步` for explicit actionable tasks.

If this session has a successful `/diary-zt` snapshot, reference its path near the opening. Do not repeat the entire transcript.
