# 设置
```
git config --global user.name "Alley"
git config --global user.email "1030184860@qq.com"
# 查看自己的配置
git config --list
```
# 知识点
## 四个区名称及含义
1. workspace 工作区
	add之前文件位于工作区，就是本地目录下，未交给git管理之前，但是在该仓库路径下的区
2. index/stage 暂存区
	add之后为暂存区
3. Repository 仓库区（本地仓库）
	commit提交
4. 远程仓库

## 常用命令
### 让git删除跟踪的文件，将文件从暂存区删除
```git rm --cached *```
### commit相关命令
```shell
# 允许提交的message为空
git commit --allow-empty-message -m ""
# 提交完之后, 进行了一些修改, 再次上次的message提交
git commit --amend -m "message"
```
### 版本退回
```shell
# 每次commit都会有log记录
git reflog # 可查看所有历史记录
git log # 可查看当前版本以及其以前的记录，以后的就不能看了
git log --pretty=oneline # 显示信息更简洁
# 版本退回与恢复实现
git reset --hard HEAD^ # 向前退回一次
git reset --hard id(需要输入大概5位才行) # 版本转为指定id的版本
```

### 删除文件
文件进行提交后，假如删除了也需要再重新提交一次才行，这样以后版本穿越还能穿越到未删除前的状态

### 远程仓库
```shell
# 添加远程库，使用origin与特定远程库关联
git remote add origin 地址
# 删除远程库
git remote rm origin
# 查看远程库
git remote -v
# 提交到远程库
git push -u origin master
# 第一次push的时候需要上面这个完整代码之后使用
git push 即可
```

## 分支管理
```shell
# 创建分支
git branch name
# 切换分支
git switch name
git checkout name
# 创建+切换分支
git branch -b name
gti switch -c name
# 合并某分支到当前分支
git merge name
# 删除分支
git branch -d name
```
