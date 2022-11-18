# YourPR
learning how to pull request

# 【开源社区】如何提交你的Pull Request (附带有测试学习用的github仓库)
> 以下流程包括了下载开源项目，到本地开发，git push以及签名，到最后github 提交PR的所有流程
> 本文提供一个可以专门用于实验github pr 的仓库，测试时指令或者是参数部分可以完全复制粘贴，但在使用的时候需要修改对应的参数
>  坚持 Code Fisrt 的原则， 先讲操作再来解释具体的术语【超级保姆教程】
>  ==本教程当中 凡是`[大写字母]`都是需要你自己的修改的地方，不能够直接复制粘贴==

@[toc]

## 一. 复制项目并下载到本地并开发

### 1. 先 Fork 目标项目
如下图所示，进入到想要开发的开源项目主页，点击右上角的fork按钮，创建出自己账号的对应克隆仓库。

<center class="half">
<img alt="fork目标仓库" class="has" height="" src="https://img-blog.csdnimg.cn/3a0e61c782764ac0b27cd970cf6b97bf.png" width="80%">
<img alt="创建 fork" class="has" height="" src="https://img-blog.csdnimg.cn/70006ffa12e749fd8e76ff444ed4f7d0.png" width="80%">
<img alt="fork成功" class="has" height="" src="https://img-blog.csdnimg.cn/81dce38e72ee489583036705882d39b1.png" width="80%">
</center>



### 2. 下载到本地开发
目前在你的账户中已经包含了 `[你的用户名]/YourPR` 仓库，需要将它克隆到本地来进行编辑。

Github 提供的下载方式如图所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/a4f9c1f66aca43e7b3231ffed88b9fe9.png#pic_center =400x340)
从选项上看包括三类下载的方式：
* `git` 指令 `clone` 
* 打开桌面应用
* 下载ZIP文件
作为工程师来说，我们大多选用第一项来作为下载仓库的方式。当然，可以从图中看到 clone 有三种方式来选择，具体形式为以下：
```shell
# 推荐使用http方式来获取源代码
git clone https://github.com/IdeaMeshDyx/YourPR.git

#这个需要配置ssh连接
git clone git@github.com:IdeaMeshDyx/YourPR.git

# 前提是安装过 gh 
gh repo clone IdeaMeshDyx/YourPR
```
会出现以上情况是因为Git 可以使用四种不同的协议来传输资料：本地协议（Local），HTTP 协议，SSH（Secure Shell）协议及 Git 协议。当连接到远程仓库的时候使用的是http或者ssh ,它们之间的具体差距可以看[服务器上的 Git - 协议](https://git-scm.com/book/zh/v2/服务器上的-Git-协议)
> 直接执行 `git clone https://github.com/IdeaMeshDyx/YourPR.git`, 可能会出现
> 无法下载成功的问题，排除加速器[不可抗环境]因素之后，找到原因之一是github 不支持http 账号密码形式的访问了，可以通过生成Token 或者是 gh 工具来实现联通，具体解决办法看以下：
>  [GitHub CLI manual](https://cli.github.com/manual/)
>  [About remote repositories](https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls)

---

## 二. 本地git开发并提供签名
此时本地已经有用于开发的仓库副本了，使用 git 进行管理，这需要了解一部分git的使用以及原理，具体可以看：
 * [Git 指令功能参数查询](https://git-scm.com/docs)
 * [Git教程- 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600)
 
当然，使用一些常见的指令就完全可以完成平时的工作了。接下来，你可以跟着文章一起编辑一些文件并添加到测试仓库当中，增加自己的账号签名或者是做其他的操作。

```bash
# 创建自己的分支
git branch [YOUR BRANCH]
git checkout [YOUR BRANCH]

# 目前YourPR 目录下面只有这个README.md 文件，可以创建自己的目录
mkdir [YOUREFILE]

# 进入这个目录
cd [YOUREFILE]

# 编写一个文档来记录一些东西
vim [YOUREFILE].txt
```

结果显示如下：
![成果](https://img-blog.csdnimg.cn/7cb40240a2d74ddda7eaa56df3783d54.png)

以上步骤替换为你正常的开发流程就可以了。

接下来就是关键步骤，需要你保存修改的内容并为之添加`commit`信息来做git管理标记，同时由于开源项目还需要标注签名以保障著作权（bushi），你需要配置好`git config` 参数

### 1. 保存修改
```bash
#查看所有的修改内容，建议每一次查看都保留对应的内容
git status

# 将所有的修改保存起来，时常使用这样才能够保障代码修改不会被丢弃
git add .
```
![结果显示](https://img-blog.csdnimg.cn/710f3e17346d4314af17535c7ac9f089.png#pic_center)


### 2. 查看log日志
```bash
# 查看 log 日志
git log

# 查看自己的 git 是否正确添加了账户信息
git config --list
```
由于没有 commit 自己的修改内容，此时查看的`git  log`信息都是之前其他人提交的修改信息，可以和之后`git log`来做对比，查看是否自己提交了，最重要的是版本管理就需要获取其中的id来做回退。

`git config --list` 需要查看目前git 保存的信息，为了能够让commit当中包含自己的账号信息，一定要保障这个git仓库的`config`当中有`user.name`以及`user.email`信息。
![config](https://img-blog.csdnimg.cn/255fa1222aab4626831f222a65fa1423.png#pic_center)
如果没有查看到这些信息的话，就需要自己的配置和添加，以下为具体方法：
```bash
# 增加自己的账号名称和邮箱
git config user.name "[YOUR GITHUB ACCOUNT]"
git config user.email "[YOUR GITHUB EMAIL]"

# 添加后再查看一次 git config --list
git config --list
```


> 每个git 仓库都可以配置自己的config信息，包括`user.name`以及`user.email`, 网上许多博客设置了 `--global`参数，这个配置的文件是当前用户组全局的，不太推荐使用。这个config其实也包括了之后提交仓库、远程代码同步的设置内容
> ```bash
> Config file location
>  --global              use global config file
>  --system              use system config file
>  --local               use repository config file
>  --worktree            use per-worktree config file
>  -f, --file <file>     use given config file
>  --blob <blob-id>      read config from given blob object`
> ```
> 

### 3. 提交带有签名的日志
在这个部分主要有两件事特别注意：
* `commit`的信息应当符合自己所提交开源仓库的代码规范，一般来说说清楚此次修改做了些啥、在哪里是最好的，也方便自己定位版本。本文提供一个参考：[Git Commit 规范](https://blog.csdn.net/benjaminparker/article/details/120942232)
* 提交的修改，应当在log当中包含config 信息，这样开源社区的其他小伙伴才知道这个是你做的修改

```bash
# 测试用的commit 信息
git commit -s -m  "feature: add new file by [YOURNAME]"

# 查看git log 信息
git log 
```
成功的话就会显示以下内容
![标注](https://img-blog.csdnimg.cn/90fd2c99022540ffae54af1f84e71137.png#pic_center=10x10)

方框的两个部分签名都正确，对应config当中设置的内容就是成功了

> 添加签名的方式有两种：
> ```bash
> git commit --signoff --message 'This is my commit message'
> # 注意这个-s 和 -m 的顺序不能乱，不然-s 会去识别“”里面的信息
> git commit -s -m "This is my commit message"
> ```
> 可以参考的文章：
> [添加 git --signoff](https://docs.pi-hole.net/guides/github/how-to-signoff/)
> 
当然，即便这里出现问题，也不用担心，可以使用`git rebase`修改log信息,这个情况也会发生在多次提交了commit信息的情况之下，想要将冗余的log信息合并删除的时候
```bash
# 将文本编辑器设置为vim ，可选，主要我用不惯nano,注意这里的--global和上文说的一致，可以自行修改
git config --global core.editor "vim"

# git rebase -i HEAD~4 后面的这个4表明要修改的log信息数量
git rebase -i HEAD~[THIS IS THE NUM OF LOGS YOU WHAT TO CHANGE]
```
> 当然这部分修改也有不少可以讲的内容【可以水/bushi】，之后再做合并，可以先参考以下文章
> [git rebase  详解](http://jartto.wang/2018/12/11/git-rebase/)
> [git rebase](https://git-scm.com/docs/git-rebase)

到这里为止，本地的版本管理内容就已经全部完成了，剩下需要学习的就是如何将本地的代码上传给github开源社区以及如何同步远程源代码仓库的一些更新内容。

## 三. 设置远程仓库并且 push
首先查看本地仓库对应的远程仓库信息

```bash
git remote -v
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/b2a9c2f3a31f46d1813e8970c9e625f7.png#pic_center)
可以看到设置的拉取远程仓库`origin` 为你自己的远程github仓库。
而参与项目开发对于远程仓库实际上有两个定位需求：

* 自己项目开发仓库：一般命名为`origin`, 是自己github 账号下面管理的仓库，push 操作都是push 到这个仓库当中，是主要的修改位置。
* 远程源代码仓库：一般命名为`upstream` ,由于咱们在开发代码的时候，其他人也不是闲着，他们也会向主仓库提交自己的代码修改，那么很可能在自己想要加新功能的时候，源代码仓库已经有很大的变化了，想要保障代码仓库的更新就需要设置同步机制

```bash
## 添加原仓库，用于同步最新的代码
# git remote add upstream [YOUR WANTED GITHUB URL]
git remote add upstream https://github.com/NKDYX/YourPR.git

# 禁止直接向 upstream 源 push，因为我们不是 dmlc 的人，没有 push 的权限，要提交代码必须通过 Pull Request，
git remote set-url --push upstream no_push

# 再通过git 查看一下
git remote -v

# 检查 upstream 源的代码最新状态，先切到本地的main 或者master 分支【主分支】,并合并
# 当然可以在这里将自己的修改merge到main 分支上面，但是这样可能会涉及更多问题，对于新手花费更多精力就不划算了，所以就只停到主分支的更新，再开发就从新的main再创建分支来做
git checkout master
git fetch upstream
git merge upstream/main

```

首先可以看到是添加了对应的仓库
![git remote -v](https://img-blog.csdnimg.cn/6b759d1e54ee4d9686b8f45fa4765fb4.png#pic_right)
当设置了不用push 的参数之后，结果显示为：
![在这里插入图片描述](https://img-blog.csdnimg.cn/086670cb0675475b849c5842c3e56324.png#pic_right)


> 这里提供一些 git merge 相关的参考，以便可以自行修改分支
> [git 好课，强推！！](https://www.atlassian.com/git/tutorials/using-branches/git-merge)
> [官方文档](https://git-scm.com/docs/git-merge)

接下来就是万众瞩目的push环节，将自己的代码先push到远程自己的复制仓库名下

```bash
git push origin 
```

