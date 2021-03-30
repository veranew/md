# git 常用命令

![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5ydWFueWlmZW5nLmNvbS9ibG9naW1nL2Fzc2V0LzIwMTUvYmcyMDE1MTIwOTAxLnBuZw?x-oss-process=image/format,png)

- Workspace：工作区
- Index / Stage：暂存区
- Repository：仓库区（或本地仓库）
- Remote：远程仓库

## **本地分支关联远程**

```bash
git branch --set-upstream-to=origin/分支名 分支名
```

## 代码库修改密码后push不上去怎么办？

```bash
// 重新输入密码
git config --system --unset credential.helper
 
// 密码存储同步
git config --global credential.helper store
```



# git版本管理

* 集中式：SVN
* 分布式：Git
----
- `mkdir` 文件夹 //创建文件夹
- `ls -a` 查看所有文件
- `vim` 文件名  查看文件
- `touch a.txt`  创建一个文件

subl .gitignore  
----

创建一个Git忽略文件

`*.txt` Git忽略.txt后缀文件

`!a.txt`  Git忽略.txt后缀文件，除了a.txt文件

`/home`   Git忽略home文件夹

`/home/*.txt`    Git忽略home中.txt后缀文件*

`*/home/**/*.txt`    Git忽略home中及子目录所有.txt后缀文件



Git指令
----

- `git init`   创建Git管理仓库
- `git add .`  所有文件提交暂存区
- `git add xxx.txt`  指定某个文件提交到暂存区
- `git commit -m ‘提交本地仓库日志’`  提交到本地仓库
- `git status` 版本管理状态
- `git clone ulr` 克隆项目到本地
- `git log`  Git提交日志
- `git checkout` 版本号 切换版本

----
`git mv a.php abc.php`  将a.php修改为abc.php,并进入暂存区（存在大小写没变=>git add .=>git commit ...）

----
简写配置:

`[alias]`
    `a = add`
    `c = commit`
     `l = log`
     `s = status`
在`.gitconfig`中配置命令别名

----
分支：

`git branch`  查看分支

`git branch -a`  查看所有分支

`git branch xxx`  创建分支xxx

`git branch --merged` 查看合并分支

`git branch --no-merged` 查看未合并分支

`git checkout xxx`  切换分支xxx

`git checkout -b xxx`  创建并切换到xxx分支

`git merge 分支名   合并分支`（提示：必须切换到master主分支上）

`git branch -d（-D）` 分支名  删除分支（删除未合并分支）

`git stash`  临时暂存

`git stash list`  查看临时暂存

`git tag` 添加标签-应用版本

`git archive master --prefix='hdcms/' --forma=zip > hdcms.zip`  生成zip压缩包hdcms

`git remote` -v 查看远程分支

----
分支开发时，master发生改变

`git rebase master`  将master分支衍合到当前分支

----
`git remote add origin(别名） 远程url`  关联远程仓库

`git push -u origin master`  推送远程仓库

`git push origin 本地分支：远程分支`  创建、推送、关联远程分支

`git pull origin 本地分支：远程分支`  创建、拉取、关联远程分支

`git push origin --delete 分支名`  删除远程分支