title: some useful git command
date: 2015-08-18 16:35:10
tags:
- git
---
## 不提交一个文件（已经在仓库中，并且不想将远程仓库中的文件删除）在本地的改变

### GIT: ignoring changes in tracked files29/01/2009
There may be times when you want to edit some variables in for example a database connection file, to run an application right from within your GIT repo. Of course you don’t wont those changes to be commited, so you add the file the .gitignore.
However adding tracked files to .gitignore won’t work because GIT will still track the changes and commit the file if you use the -a parameter.
Fortunately GIT has a very easy solution for this, just run the following command on the file or path you want to ignore the changes of:
> `git update-index --assume-unchanged <file>`    

If you wanna start tracking changes again run the following command:
> `git update-index --no-assume-unchanged <file>`


### 参考资料：
http://blog.pagebakers.nl/2009/01/29/git-ignoring-changes-in-tracked-files/