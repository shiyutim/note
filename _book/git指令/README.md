1. `ls` 当前文件 
2. `pwd`用于显示当前目录
3. `git config --global user.name ''  ` 【设置用户名（跟github一样）】
4. `git config --global user.email ''  ` 【设置邮箱（跟github一样）】
5. `git config --global --list`【查看user name and email】
6. `mkdir <文件夹名字>`【建立文件夹】
7. `cd <文件夹名字>`【进入文件夹】
8. `git init`【将该目录变成git仓库】
9. `touch <文件名字>`  【创建文件】
10. `git add <文件名字>`  【把文件提交暂存区】
11. `git commit -m ''` (引号中是提交文件的描述)  【将文件从暂存区提交到仓库】
12. `vim <文件名字>`  【进入文件编辑 】【按i进行开始编辑 】【按esc然后输入：wq 退出编辑】

## 把文件上传到github步骤
1. `git clone <github仓库地址>`  【把github仓库克隆到本地】
2. 进入文件夹后，创建文件
3. `git add` 
4. `git commit -m ''`
5. `git push`


#### 其他命令
1. local比global优先级高
2. `clear`【清除历史记录】
3. `ls -al`【查看文件目录】
4. `git status` 【查看状态】
5. `rm -rf` [文件名]  【删除文件】
6. `git rm <文件名>` 【删除暂存区文件】
7. `cd ..\`  【返回上一层】
8. `git reset HEAD`【把提交到暂存区的文件恢复到本地】
9. `git log`【查看历史提交记录】
10. `git diff`【对比文件】
11. `git mv <旧文件名> <新文件名>`【重命名文件】



#### 切换分支
1. 查看远程分支`git branch -a`
2. 查看本地分支`git branch`
3. 切换分支`git checkout -b <分支名>`
4. 切换回master`git checkout master`

