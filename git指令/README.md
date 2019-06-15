# Git指令
1. `ls` **当前文件**
2. `pwd`**用于显示当前目录**
3. `git config --global user.name '用户名'` **你的Github用户名**
4. `git config --global user.email 'email'` **你的Github邮箱**
5. `git config --global --list` **查看user name and email**
6. `mkdir <文件夹>` **创建文件夹**
7. `cd <文件夹>`**进入文件夹**
8. `git init` **将该目录变成git仓库**
9. `touch <文件夹>` **创建文件**
10. `git add <文件夹>` **把文件提交暂存区**
11. `git commit -m ''`**将文件从暂存区提交到仓库**
12. `vim <文件>` **可以进入文件编辑，按i开始编辑，按esc然后输入：wq退出编辑**
---
### 将文件上传到github步骤
1. `git add <文件名>` 
2. `git commit -m ''`
3. `git push`

---

### 其他指令
1. `clear`清除历史记录
2. `ls -al` 查看文件目录
3. `git status`查看文件状态
4. `rm -rf <文件名>`删除文件
5. `git rm <文件名>` 删除暂存区文件
6. `cd ../`返回上一层