【一小时Git教程】 https://www.bilibili.com/video/BV1HM411377j

git config --global --list
git log 查看提交记录。可选参数 --oneline
git reflog 列出所有版本，以供reset
git ls-files查看暂存区内容。

git reset 如下：soft hard mixed
以下是一个提交了3次的文件夹。上个版本的记录是commit 5af90b8

git reset --soft 5af90b8

ls: 工作区file3存在 git ls-files 暂存区file3存在。

git status: 提示file3是将要提交的变更，可以git restore --staged file3来撤销暂存。

思考：相当于已经add尚未commit。也就是仅进行撤销提交的操作。



git reset --hard HEAD^

ls: file3文件不存在。暂存区也不存在。



git reset HEAD^

即使用默认选项 --mixed

file3在工作区存在，暂存区不存在。要重新add才能进入暂存区。



