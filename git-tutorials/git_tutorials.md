# 一、创建版本库

## 1. 选择合适的地方，创建一个空的目录

```
$ mkdir 文件名   # 创建一个文件夹
$ cd 文件名路径  # 路径操作
$ pwd            # 显示当前路径
```
## 2. 通过`git init`命令把这个目录变成 Git 可以管理的仓库

`$ git init`
运行完以后

```
Initialized empty Git repository in C:/git/.git/
```
产生一个空的文件夹，里面有一个 `.git` 文件夹（**注意：这个目录是Git来跟踪管理版本库的，没事千万不要⼿动修改这个目录⾥⾯ 的⽂件，不然改乱了，就把Git仓库给破坏了。**）

### 3. 把文件添加到版本库

所有的版本控制系统，其实只能跟踪⽂本⽂件的改动，⽐如TXT⽂
件，⺴⻚，所有的程序代码等等，Git 也不例外。版本控制系统可以告诉你每次的改动，⽐如在第5⾏加了⼀个单词“Linux”，在第8⾏删了⼀个单词“Windows”。⽽图⽚、视频这些⼆进制⽂件，虽然也能由版本 控制系统管理，但没法跟踪⽂件的变化，只能把⼆进制⽂件每次改动串起来，也就是只知道图⽚从100KB改成了120KB，但到底改了啥，版本控制系统不知 道，也没法知道。**Window 系统不要用自带的记事本编辑，用 Notepad++ 代替，记得把Notepad++的默认编码设置为UTF-8 without BOM即可**

主要命令：
```
$ git add filename/folder   # 把文件名或者文件夹名添加到仓库
```
⽤命令`git commit`告诉 Git，把⽂件提交到仓库
```
$ git commit -m "描述"
```



# 二、 添加远程库

本地创建好一个 Git 仓库后，同时也想在 Github 上创建 Git 仓库，并让两个仓库进行远程同步，这样 Github 上的仓库既可以做备份，也可以让其他人通过该仓库进行合作，一举多得。具体步骤如下：
- 登入 Github ，点击创建仓库( NEW )，然后输入仓库名(Repository name),最后点击 Creat Repository 创建成功。不选择生成 Readme.md 的话，系统会生成一些 Git 代码，指导你进行操作。如：（我创建的仓库名叫 `git-learning` ）
```
…or create a new repository on the command line
echo "# git-learning" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/FLyingLSJ/git-learning.git
git push -u origin master
…or push an existing repository from the command line
git remote add origin https://github.com/FLyingLSJ/git-learning.git
git push -u origin master
…or import code from another repository
You can initialize this repository with code from a Subversion, Mercurial, or TFS project.
```
- 创建成功后， Github 上的仓库还是空的。 Github 告诉我们，可以从这个仓库克隆
  出新的仓库，也可以把⼀个已有的本地仓库与之关联，然后，把本地仓库的内容推送到 GitHub 仓库。
1. 在本地的 git-learning 仓库运行以下代码（记住，要在 Git Bush 上把路径定位到你本地的仓库中即运行 `cd 仓库的路径`）
```
$ git remote add origin https://github.com/FLyingLSJ/git-learning.git
```
2. 添加后，远程仓库的名字就是 origin 这是 Git 默认的叫法，也可以改成其他的，但是这个名字一看就知道是远程仓库。
3. 现在就可以把本地仓库所有内容推送到远程仓库上。我的运行结果
```
$  git push -u origin master
Enumerating objects: 13, done.
Counting objects: 100% (13/13), done.
Delta compression using up to 4 threads
Compressing objects: 100% (9/9), done.
Writing objects: 100% (13/13), 1.04 KiB | 531.00 KiB/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), done.
remote:
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/FLyingLSJ/git-learning/pull/new/master
remote:
To https://github.com/FLyingLSJ/git-learning.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```
把本地仓库推送到远程，用 `git push` 命令，实际上是把当前分⽀ master 推送到远程。
4. 由于远程库是空的，我们第⼀次推送 master 分⽀时，加上了 `-u` 参数， Git 不但会把本地的
    master 分⽀内容推送的远程新的 master 分⽀，还会把本地的 master 分⽀和远程的 master
    分⽀关联起来，在以后的推送或者拉取时就可以简化命令。
5. 推送成功后就在 Github 页面中看到远程仓库和本地仓库一模一样。
6. 现在，只要在本地作了提交，可以通过命令
```
$ git push origin master
```
把本地 master 分支最新修改推送到 Github。

- 总结
1. 要关联⼀个远程库，使⽤命令
```
git remote add origin git@server-name:path/repo-name.git
```
2. 关联后，使⽤命令
```
git push -u origin
```
master 第⼀次推送 master 分⽀的所有内容；
3. 此后，每次本地提交后，只要有必要，就可以使⽤命令
```
git push origin master
```
推送最新修改；

分布式版本系统的最⼤好处之⼀是在本地⼯作完全不需要考虑远程库的存在，也就是有没有联系都可以正常⼯作，⽽SVN在没有联⺴的时候是拒绝干活的！当有网络的时候，再把本地提交推送⼀下就完成了同步，真是太⽅便了



# 三、 修改远程仓库名称

1. 在本地仓库删除远程仓库：

```
git remote rm origin  
```
2. 修改 Github 仓库名称： 
  在 Github 页面中，进入要修改的仓库，在页面上方选择“Settings”，即可重命名远程仓库。

 3 添加新的远程仓库：

```
git remote add origin git@github.com:your_account_name/new_repo_name.git 
```