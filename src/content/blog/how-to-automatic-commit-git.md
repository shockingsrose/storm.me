---
author: Ryan Zhou
pubDatetime: 2024-11-22T03:37:34.948Z
title: Automatic commit to Git
slug: Automatic commit to Git
featured: true
draft: false
tags:
  - docs
description: Help you automatic push of git commits
---

# 如何自动提交 Git：确保 Markdown 文件的实时同步

在如今的信息化时代，保持数据同步变得越来越重要。作为一名使用 Typora 编写 Markdown 的用户，我希望能够在公司和家里方便地访问我的笔记。为了满足这一需求，我创建了一个 GitHub 仓库来存储所有 Markdown 文件。尽管如此，每次编辑后手动推送更改仍然是一个麻烦。因此，我决定使用 macOS 的 crontab 命令，每隔 10 分钟自动提交并推送我的更改。

## 遇到的问题

在手动管理 Markdown 文件到 GitHub 的过程中，我遇到了一些挑战：

1. **重复的手动操作**：每次编辑完成后，我需要记得执行 Git 命令，这容易导致数据的不一致。
2. **忘记提交**：有时候我会忘记将更改提交和推送到远程仓库，导致数据不同步。

为了解决这些问题，我决定: 使用自动化脚本来处理 Git 提交和推送。

## 解决方案：使用 crontab 和自动脚本

### 第一步：编写 autoSave.sh 脚本

首先，我们需要创建一个名为 `autoSave.sh` 的脚本。可以在任意文本编辑器中打开一个新文件，粘贴以下内容：

```bash
#!/bin/bash
cd ~/Markdown # 替换为你的 Markdown 文件夹路径
git add .
git commit -m "auto save"
git push -u origin master
```

请确保将 `~/Markdown` 替换为你的实际 Markdown 文件夹路径。

### 第二步：给予脚本执行权限

接下来，我们需要给这个脚本添加执行权限。在终端中，运行以下命令：

```bash
chmod +x ~/path/to/your/autoSave.sh
```

替换 `~/path/to/your/` 为你的脚本实际存放路径。

### 第三步：设置 crontab 定时任务

然后，我们可以使用 crontab 来设置定时任务。打开终端并输入：

```bash
crontab -e
```

在打开的编辑器中，添加以下行，这里设置为每隔 1 分钟执行一次：

```bash
* * * * * /path/to/your/autoSave.sh
```

确保将 `/path/to/your/` 替换为你存放 `autoSave.sh` 脚本的完整路径。

### 第四步：保存并退出

保存并退出编辑器（在 Vim 中按 Esc 然后输入 `:wq`），crontab 将会更新并开始运行。

## 注意事项

- **确保 Git 设置正确**：确保你在仓库中已经设置好了 Git 用户名和邮箱，并且 SSH 密钥已正确配置，以便可以无密码推送。

## 结论

通过这种方式，您可以有效地保持自己 Markdown 文件的同步，减少手动操作的负担。自动提交 Git 是一种便利的做法，它帮助我随时随地访问我的笔记，而不必担心数据的不同步。希望这篇文章能对你有所帮助！如果你有任何问题或想法，欢迎在评论区留言。

---

希望这篇文章能够帮助你顺利完成博客的撰写！如果你有其他想法或者需要进一步的帮助，请随时告诉我。
