# diary-zt 设计

`/diary-zt` 是两步完整快照：先提议文件名和路径，用户确认后写入。新标题会重新提议，取消不写入。`/diary-zt-a` 只追加已有文件中的新增会话内容。

运行时配置在用户主目录的 `diary-zt/current_path.txt`。配置缺失、为空或指向缺失目录时，创建 `<home>/diary-zt/yearYYYY/MM/` 作为默认目录。包本身不包含个人配置或会话数据。
