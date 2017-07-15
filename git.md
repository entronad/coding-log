git status    当前状态

git diff

git log

HEAD    当前版本

HEAD^    上一版本

HEAD^^    上两版本

HEAD~10    上10版本

git reset HEAD/哈希

git reflog    每一条命令的hash和内容

git checkout -- 文件名    放弃该文件的修改回到最近的暂存区

git reset HEAD 文件名    将HEAD之后暂存区的修改撤销掉，不会动工作区，用git checkout -- 文件名    撤销工作区

-u    即--set-upstream，第一次push时关联分支

---

git checkout -b dev    等价于：

​	git branch dev    创建分支

​	git checkout dev    切换到分支

git branch    查看所有分支

git merge    合并指定分支到当前分支

git branch -d 分支名    删除分支

git log --graph    带图形的log

git merge --no-ff -m "提交信息" 分支名    合并指定分支到当前分支保留提交信息

---

git stash    将当前工作区内容储存并清空

git stash list    查看当前stash

git stash pop   恢复stash中的内容到当前工作区，等价于：

​	git stash apply

​	git stash drop

---

git branch -D 分支名    强制删除未合并的分支

---

git remote [-v]    查看远程信息

git clone只能拿到远程仓库的当前分支，另外的分支要：

git checkout -b 分支名 origin/分支名

---

git tag    查看所有标签，按字母排序

git tag 标签名 [哈希]    给当前/指定提交打标签

git tag -a 标签名 -m 提交信息 [哈希]    打标签时提交信息

git show 标签名    查看标签详情

git tag -d 标签名    删除本地标签

git push origin 标签名/--tags    推送标签/全部标签

删除已推送到远程的标签：

​	git tag -d 标签名

​	git push origin :refs/tags/标签名



