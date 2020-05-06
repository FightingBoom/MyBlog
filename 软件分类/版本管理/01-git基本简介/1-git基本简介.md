> 道阻且长，行则将至。埋头苦干，不鸣则已，一鸣惊人！加油，骚年！

# 1 前言
&emsp;&emsp;说实话，我刚开始也不知道git到底是什么，更不明白 git、GitLab、GitHub 之间到底有什么联系，又有什么不同，所以就感觉很恐惧，一点都不了解这是啥，我要怎么用？

&emsp;&emsp;git 官网：[git官网](https://git-scm.com/)

## 1.1 初探Git
&emsp;&emsp;然后工作这1年多，也全部使用的是 SVN，也没接触过 git，不过后来老大说后边我们部门也要转到 git，使用 git 来管理源码。然后要我们提前自学一下，然后给了个网站，是廖雪峰老师的网站教程，参考这个网站：[廖雪峰git教程](https://www.liaoxuefeng.com/wiki/896043488029600)。奈何当时看了网站的教程，没有记录电子笔记，现在想看看自己当时的笔记内容，突然发现找不到笔记本了:cry:，甚是遗憾。

&emsp;&emsp;简单回忆一下廖雪峰老师的教程
 - 权威，专业；当时我看到我们老大发的这个网站的时候，就感觉有一种似曾相识的感觉（我原来不是纯软件），然后总觉得在哪里听过这个老师的名字，可能这就是:cow:人吧！
 - 教程详细，内容通俗易懂；
 - 这份教程，给我的感觉就像一本书目录一样，哪里不会，直接翻到对应目录，进行点对点突破。
 - 最后总结，值得收藏翻阅！

## 1.2 Git再进宫:fist:
&emsp;&emsp;不过也刚好，促使我自己又重新学习，记录了一遍，然后自己自学过程中，参考的是黑马程序员的教程，参考这个网站：[Git零基础入门到实战详解](https://www.bilibili.com/video/BV1sJ411D7xN?p=1)。

&emsp;&emsp;也简单总结一下黑马程序员老师的这份教程
 - 很，特别，十分基础；老师简直就是0基础教学一样。（这也导致我前5节课，基本没记什么笔记:joy:）
 - 前边也说了，老师讲课的内容，十分基础，这也导致了老师的语速，特别慢！！！基本全程1.5倍速，遇到重点会暂停下来，进行实操。
 - 总得来说，还不错，起码有老师带着，系统的过了一遍，然后该倍速的倍速就好了。

# 2 git是什么？
&emsp;&emsp;根据 git 官网介绍如下：
> Git 是一个免费的、开源的分布式版本控制系统，可以快速高效地处理从小型到大型的项目。
Git 很容易学习，而且它的足迹很小，性能非常好。它超越了 Subversion、CVS、Perforce 和ClearCase 等 SCM 工具，具有廉价的本地分支、方便的暂存区域和多个工作流等特性。

&emsp;&emsp;简单的说，就是一个版本控制系统，类似常见到的版本修改说明表，不过这个可以借助于软件来帮助我们实现版本控制，很方便。

&emsp;&emsp;想要再具体的解释，可以参考廖雪峰老师的 git 简介，上边举的例子也很通俗易懂。传送门：[廖雪峰老师 - Git简介](https://www.liaoxuefeng.com/wiki/896043488029600/896067008724000)


# 3 git使用
## 3.1 安装过程
&emsp;&emsp;直接去官网下载最新版本的 git ，安装过程呢，依我百度这么多经验来看，==一路 next 即可！==

&emsp;&emsp;实在不会的，点击这个传送门:point_right:：[Window10下安装Git](https://blog.csdn.net/qq_32786873/article/details/80570783)

&emsp;&emsp;安装完成后，鼠标右键应该会有这两个东东

![image-20200506204020002](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200506204021.png)

```shell
Git GUI Here
Git Bash Here
```

&emsp;&emsp;有上述图标，则代表已经安装完成了！可以开始使用了。

## 3.2 本地操作工作流程

&emsp;&emsp;按照黑马老师的讲解，应该有三个地方，两个步骤，首先是添加要提交的文件，然后执行提交操作（此时需要写上日志）。

&emsp;&emsp;参考截图如下：

![image-20200506204358899](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200506210249.png)

&emsp;&emsp;具体步骤，简要总结如下
```shell
git add .			// 添加当前目录下所有文件
git add filename	// 添加对应文件

git status			// 查看当前状态，非必选

git commit -m "1、这个地方写提交日志文件"
```

## 3.3 本地仓库操作

### 3.3.1 设置用户

&emsp;&emsp;当安装完成后，我们就可以在本地建一个单独的文件夹，进行 git 文件的存放及管理；
&emsp;&emsp;此时需要先进行全局配置，简单的说就是需要使用用户登录，好让其他人知道这台电脑上，是谁在修改这个文件，提交的人是谁，此时可以使用如下两条命令
```shell
git config --global user.name "用户名"
git config --global user.email "邮箱地址"
```

### 3.3.2 git仓库初始化
&emsp;&emsp;当我们建立一个单独的 git 仓库文件夹后，还需要对此目录进行初始化，需要让 git 知道要管理这个目录，使用如下命令
```shell
git init
```

### 3.3.3 实际练习
&emsp;&emsp;当一切准备就绪后，就可以按照上边的流程，实际测试一下了，比如我们新建了一个 ReadMe 文件，就可以按照如下方法，进行提交到本地仓库

![image-20200506210735620](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200506210844.png)

### 3.3.4 补充说明
&emsp;&emsp;使用 git 添加文件时，可以一次添加多个文件，这个和 Linux 的基本操作比较类似，如下
```shell
git add .				// 添加当前目录下所有文件
git add filename1		// 添加第一个文件
git add filename1 filename2 filename3 ...	// 一次添加多个文件到缓存区
```



# 3.4 git 版本回退

&emsp;&emsp;实际使用中，如果需要回退到之前版本，应该如何去做？

- 首先需要查看历史版本，也就是常说的日志，确定时间点及想要回退到的版本号；
- 查看日志，可以使用如下命令

```shell
git log						// 查看日志信息，详细信息
git log --pretty=oneline	// 显示日志的简略信息，只显示版本号和提交日志
```

- 两种查看日志方法，效果如下

![image-20200506214220333](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200506214432.png)



![image-20200506214248668](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200506214433.png)



- 然后可以使用如下命令，回退到之前版本

```shell
git reset --hard 版本号
```

- 其中版本号就是日志文件那一长串的字母+数字，这个看起来很长，但是写的时候，没必要全部都写，如果你目前在用 GitHub 的话，可以在上边看到，一般只取==前7个字符即可==。



&emsp;&emsp;问题来了，如果回退到之前的版本后，再想要回到**原来最新的版本**，怎么办？此时再使用 <font color=#ff0000>`git log`</font> 命令就会发现，看不到相关日志，怎么办？



&emsp;&emsp;git 还提供了另外一个查看日志的命令

```shell
git reflog
```

&emsp;&emsp;此时得到相关的版本号，即可再次使用 <font color=#ff0000>`git reset --hard 版本号`</font> 命令，到对应版本。



# 4 总结

1. 要想回到过去，必须先得到 <font color=#ff0000>`commit id`</font>（版本号）；
2. 要回到未来，需要使用 <font color=#ff0000>`git reflog`</font> 命令进行历史操作查看，得到对应版本号；
3. 版本号可以不用写全，一般为7个字符即可。