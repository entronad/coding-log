commit格式：

动词（add/update/fix）+ 内容 + at/in/of + 文件/模块 + [[fixed/closed] #issue号码]

c.f. continue from下次从何处开始

中间用 | 间隔

版本节点

[release/build/test] 1.0.1

coding-log

修改的文件名



git status    当前状态

git diff

git log

HEAD    当前版本

HEAD^    上一版本

HEAD^^    上两版本

HEAD~10    上10版本

git reset HEAD/哈希 退回到某一版本

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

git branch -D 分支名    强制删除分支

git log --graph    带图形的log

git merge --no-ff -m "提交信息" 分支名    合并指定分支到当前分支保留提交信息

git push origin local_branch:remote_branch 把本地分支推送到远程的对应分支，没有就创建

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

---

设置全局不转换LF与CRLF

git config --global core.autocrlf false

---

查看当前目录下代码行数：

find . |xargs grep -v "^$"|wc -l

---

当使用HTTPS时，可通过如下方式带上用户名密码，以不用每次都输入：

```
http://yourname:password@gitee.com/name/project.git
```

如需修改：

```
git remote rm origin
```

增加https远程仓库地址

```
git remote add origin http://yourname:password@gitee.com/name/project.git
```
添加或修改.gitignore后需执行

```
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```

清一下缓存



git 默认是忽略文件名的大小写的，如改动了文件名的大小写需执行

git config core.ignorecase false



git worktree

```
git worktree add [-f] [--detach] [--checkout] [--lock] [-b <new-branch>] <path> [<commit-ish>]
```

不加commit-ish会新建一个分支，分支名为路径最终文件夹名

commit-ish为分支名，分支会被checkout在新文件夹中

当前分支不可在新文件夹中checkout

一个分支只可在一个文件夹中被checkout

总之，worktree虽然在不同文件夹中，但还是隶属于同一个.git

remove等功能需在1.17.1版本后使用

不能放在当前文件夹（即repo），新文件夹也会被追踪，建议与当前repo文件夹同级



改名

mv 命令可改文件的名称，包括只改大小写

改文件夹名称后面需跟上/

改文件夹名等同于移动原文件夹的所有文件

改文件夹名不可直接改大小写



# 在其他库基础上创建新仓库，留一个分支关联源仓库以便merge源仓库未来的改动

```
// 比如你想基于antd，创建一个新仓库antd-plus

// 首先在服务器端建立空的仓库antd-plus
// 在本地新建一个空的antd-plus文件夹，进入该文件夹

git init

// 添加两个远程仓库

git remote add origin <antd-plus url>
git remote add antd <antd url>

// fetch 并 merge antd/master 的代码

git pull antd master

// fetch antd-plus；将 master 的内容push到antd-plus/master；并将master转为关联antd-plus/master

git fetch origin
git push origin master
git branch -u origin/master master

// 创建antd分支并关联antd/master

git checkout -b antd
git branch -u antd/master antd


```

