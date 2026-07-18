# diary-zt 设计

`/diary-zt` 总是创建完整快照；`/diary-zt-a` 仅追加当前会话上一次成功日记命令之后的可见内容。运行时配置位于当前用户主目录下的 `diary-zt/current_path.txt`，而不是仓库中。

保存位置优先使用该配置所指向的既有目录。配置缺失、为空或指向缺失目录时，创建并使用 `<home>/diary-zt/yearYYYY/MM/`。主目录由平台解析，因此适用于 Windows、macOS 和 Linux。

包本身不保存任何会话或个人配置；它可安全提交到 GitHub。
