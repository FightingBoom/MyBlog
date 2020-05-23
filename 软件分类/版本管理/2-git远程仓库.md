> 道阻且长，行则将至。埋头苦干，不鸣则已，一鸣惊人！加油，骚年！

# 1 git远程仓库的创建

&emsp;&emsp;git 的远程仓库，其实就是 GitHub ，在使用 git 之前，我们就应该有了 GitHub 的账号，如果还没有的话，可以直接去官网注册。

&emsp;&emsp;创建远程仓库的步骤也很简单，在个人主页，直接点击 **New** 即可，如下图：

![image-20200523184214309](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200523184241.png)

&emsp;&emsp;接下来就是填写一些基本信息等，需要注意的是：==GitHub 不允许有空的仓库、或空的文件夹，如果此仓库/文件夹下没有内容，则会创建失败。==

![image-20200523184819376](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200523184837.png)

&emsp;&emsp;如果不在创建仓库时，默认创建一个 ReadMe 文件，则在创建仓库成功后，还是需要创建一个文件的。



# 2 使用 HTTPS 协议

&emsp;&emsp;GitHub 给我们提供了两种方式克隆仓库，一种是 HTTPS 协议，一种是 ssh 协议。两种协议都可以，后边会简单介绍一下两种协议的区别。

&emsp;&emsp;使用 HTTPS 协议时，直接进入到仓库，点击<font color=#ff0000 size=3> `Clone or download` </font>，选中<font color=#ff0000 size=3> `Use HTTPS` </font>，然后出现如下图界面，直接点击网址后边小按钮，即可完成复制。

![image-20200523191326576](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200523191326.png)

&emsp;&emsp;接着到本地对应文件夹下，打开 **git bash** ，然后使用如下命令：

```shell
git clone https://github.com/FightingBoom/MyBlog.git
```

> 注意：如果我们的仓库是空的，则在克隆时，会提示克隆了一个空仓库到本地。

&emsp;&emsp;当成功克隆仓库到本地后，就可以在本地做一些相应的操作，基本过程和本地仓库一样，不过多了最后一步 **git push** 。把基本流程再次描述如下：

```shell
// 添加文件到缓冲区
git add filenamae

// 可选：查看当前提交状态
git status

// 提交文件到缓冲区
git commit -m "此处是版本修改说明，必须写"

// push文件到远程仓库（第一次使用可能需要登录账号密码）
// 容易受网速影响，如下图，第一次push超时
git push
```

&emsp;&emsp;上边的步骤都是从本地提交/推送到远程仓库，那怎么从远程仓库获取内容呢？git 提供了如下命令：

```shell
git pull
```

&emsp;&emsp;我们可以在**对应路径**下，使用此命令，拉去远程仓库**相同路径**下的所有**有改变的内容**。



# 3 使用 SSH 协议

&emsp;&emsp;使用 SSH 协议，就相当于把自己在使用的电脑添加到 GitHub 的白名单中，这样后续在此电脑上就可以直接操作远程 GitHub 仓库，而无需每次都要登录账号密码。

&emsp;&emsp;这个方式和之前我的[利用 GitHub + PicGo + Typora 搭建属于自己的图床](https://blog.csdn.net/Fighting_Boom/article/details/105741739)，这篇文章中使用的方式刚好相反，不过原理都大差不差。具体操作步骤如下：

# 3.1 创建本地电脑SSH Key

&emsp;&emsp;可同步参考廖雪峰老师的教程，点击这个传送门:point_right:：[远程仓库](https://www.liaoxuefeng.com/wiki/896043488029600/896954117292416)

&emsp;&emsp;在本地仓库文件夹内，打开 **git bash** ，然后输入如下命令，后边的是自己注册 GitHub 账号时的邮箱名。

```shell
ssh-keygen -t rsa -C "youremail@example.com"
```

&emsp;&emsp;使用上述命令，可以一路回车，全部使用默认参数即可，当执行完毕后，可以在用户主目录下，找到 **.ssh** ，这个文件夹，路径参考下图：

![image-20200523194246222](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200523194321.png)

&emsp;&emsp;在此文件夹下，可以看到<font color=#ff0000 size=3> `id_rsa` </font> 和<font color=#ff0000 size=3> `id_rsa.pub` </font>这两个文件，需要注意的是：

1. <font color=#ff0000 size=3> `id_rsa` </font> 是私钥，不能告诉任何人；
2. <font color=#ff0000 size=3> `id_rsa.pub` </font>是公钥，可以告诉别人；

&emsp;&emsp;接下来就要去 GitHub 上添加本地电脑的公钥，这个是一个**鉴权**操作，目的就是为了让 GitHub 知道，是谁在进行操作，也就相当于添加到白名单当中。

&emsp;&emsp;具体步骤简要总结如下：

1. 点击个人头像，找到<font color=#ff0000 size=3> `Settings` </font>
2. 点击<font color=#ff0000 size=3> `SSH and GPG keys` </font>
3. 点击<font color=#ff0000 size=3> `New SSH key` </font>
4. 按照如下图示，依次添加必要的内容，即可。

![image-20200523210138190](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200523210358.png)

![image-20200523210347658](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200523210347.png)

&emsp;&emsp;添加完毕后，就可以去复制 SSH 克隆的网址了，然后用同样的步骤在本地进行测试，如果成功推送/拉去，则 GitHub 上的公钥会变成绿颜色，并显示出来在什么时候使用的等等。

![image-20200523210637567](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200523210637.png)

# 4 HTTPS 协议与 SSH 协议区别

&emsp;&emsp;参考廖雪峰老师的网站介绍，网址传送门：[从远程库克隆](https://www.liaoxuefeng.com/wiki/896043488029600/898732792973664)，两者的区别，参考如下截图：

![image-20200523190854465](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200523190854.png)

&emsp;&emsp;所以如何选择，主要还是看自己啦，不过目前比较常用的就是 SSH 协议；

&emsp;&emsp;根据老师内容，简单总结区别如下：

|   协议    | 速度 |              备注              |
| :-------: | :--: | :----------------------------: |
|  SSH协议  | 较快 |     一次设置，后续无需更改     |
| HTTPS协议 | 稍慢 | 每次推送均需要输入账号密码验证 |



# 5 总结

1. 本节主要学会了两种克隆的方法，一种是 HTTPS 协议，一种是 SSH 协议；
2. 简单了解了两种协议的操作步骤，及各自的特点；
3. 关于推送提交等内容，学习不够深入；
4. 本节课推送的分支全部为 master 分支，后续需要学习多分支操作等。

> 如果文章内容有误，麻烦评论/私信多多指教，谢谢！如果觉得文章内容还不错，留个赞呗，您的点赞就是对我最大的鼓励，谢谢您嘞！