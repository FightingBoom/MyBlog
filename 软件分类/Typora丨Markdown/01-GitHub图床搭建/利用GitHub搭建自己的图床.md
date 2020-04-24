> 道阻且长，行则将至。埋头苦干，不鸣则已，一鸣惊人！加油，骚年！！！

# 1 前言&基本介绍
&emsp;&emsp;之前直接在网页上用Markdown写博客，可以直接复制粘贴。但是现在发现了 Typora 这么好一个 Markdown 编辑器后，就想在本地写博客了，然后上传到 GitHub 上备份。

&emsp;&emsp;但是在本地写博客，总不能不插入图片吧？但是插入图片，上传到GitHub时，图片不显示怎么办？这个问题困扰了我好几天，今天终于搞定了，一定要写篇博客记录一下！

## 1.1 整体方案
&emsp;&emsp;整体上使用的是：GitHub + Typora + PicGo 来实现。

## 1.2 参考网址
&emsp;&emsp;在实现我想要的功能的时候，参考了几个很有用的博客，但他们的文章跟我自己想要的方案并不完全一样，所以我自己就参考他们的文章，总结出自己的经验。

&emsp;&emsp;1、相当于启蒙的文章：[一款markdown编辑器typora和图床的搭建过程](https://www.itcodemonkey.com/article/14536.html)

&emsp;&emsp;2、不过这个使用的是 Gitee：[windows本地markdown环境配置：使用typora，并实现图片自动插入并上传图床](https://blog.csdn.net/WinterShiver/article/details/105387744)

&emsp;&emsp;3、这个是第二篇文章中的链接，排坑用的：[手把手教你用Typora自动上传到picgo图床【教程与排坑】](https://zhuanlan.zhihu.com/p/114175770)

## 1.3 软件下载地址
1. Typora 官网：[Typora](http://typora.io/)
2. 上不去官网的，可以直接使用国内的软件管家，然后在软件内升级到最新版本即可。例如我用的腾讯电脑管家 -> 软件管家：
![image-20200423195330297](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200423195333.png)

3. PicGo 蓝奏云下载地址：[PicGo-Setup-2.2.2.exe](https://www.lanzous.com/ia49ojg)
4. PicGo 在 GitHub 上的地址：[GitHub - PicGo](https://github.com/Molunerfinn/PicGo/releases)

5. node.js 插件下载地址：[node.js下载](http://nodejs.cn/download/)

6. 没有 GitHub 账号的，自己需要先注册一个账号~

&emsp;&emsp;做好上边的准备工作，下边开始配置步骤~

# 2 GItHub
## 2.1 创建图片库
&emsp;&emsp;在自己的 GitHub 上创建一个库，当做图床，专门用来存储图片。具体操作流程与建仓库的流程一样。

&emsp;&emsp;<font color=#ff0000 size=4>由于 GitHub 不允许存在空的仓库，也不允许存在空的文件夹，因此可以勾选默认创建一个 ReadMe 文件 </font>

![1](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200423225809.png)

## 2.2 获取令牌
&emsp;&emsp;GitHub 的令牌，其实就是 token，自我感觉就像自己的 GitHub 对外的一个公钥一样，可以让拥有此 token 的软件访问 GitHub 的 API 接口。

&emsp;&emsp;生成过程，参考经验即可，大致步骤如下：
 - 点击自己的 GitHub 头像
 - Settings
 - Developer settings
 - Personal access tokens
 - Generate new token

&emsp;&emsp;如下图，注意下边的选项全部勾选。（具体不清楚，大概是赋予使用此 token 的软件一些权限）
![image-20200423231841387](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200423233041.png)

&emsp;&emsp;此时可以保存备用，也可以在下边用到的时候，再按照上述步骤生成 token 。==注意 token 是私密的，需要做好安全保护！==

# 3 本地配置步骤
## 3.1 安装配置PicGo
&emsp;&emsp;win10 电脑，直接安装下载下来的 EXE 文件即可，整个安装步骤一路 next 。

&emsp;&emsp;安装后的软件界面如下：

![image-20200424214100076](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200424214102.png)

 - 接下来配置 GitHub 作为图床，在左侧找到**图床设置**，找到**GitHub图床**。

 - 前边有星号的为必填项，依次填入之前创建的仓库名，注意是：==账户名/仓库名==；

 - 然后填入设定的分支名（创建仓库时如果没有创建其他分支，默认就是 master 分支）；

 - 最后填入之前生成的 token 令牌，点击确定。

![image-20200424214338329](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200424222337.png)

 - 然后找到 PicGo 设置，打开里边的***时间戳重命名***，这样可以避免图床在上传文件时，由于文件名相同造成的错误。

 - 然后剩下的配置项可以不用管，参考的文章不建议设置为开机自启，因为等会配置好 typora 后，typora 再上传图片时会自动打开 PicGo 软件。

## 3.2 安装配置node.js
&emsp;&emsp;这个我具体不知道是什么东西，不过我对于不知道的东西，还是踩着前人的脚印前进吧，后续有时间在深入了解。

&emsp;&emsp;整个安装过程也很简单，一路 next ，全部使用默认配置即可。

## 3.3 测试PicGo

&emsp;&emsp;到这一步，可以打开软件，直接拖动到首页上传区，测试是否上传成功；或者直接利用截图，然后点击右下角的==剪贴板图片上传==，即可快速实现上传。

&emsp;&emsp;经过实际验证，有一些理解：
1. 在上传时，如果进度条到一半出现红色，代表上传失败；
2. 在上传时，如果进度条一直是蓝色，应该就是上传成功了；
3. 在<font color=#ff0000 size=3>`PicGo设置`</font>此选项下，可以找到对应的日志文件，查看相关错误信息，进而辅助我们排查问题。

## 3.3 安装配置Typora
&emsp;&emsp;Typora 的安装教程，应该也可以一路 next。。。我自己当时直接用的软件安装管家，然后后续在软件内更新到最新版即可。

&emsp;&emsp;安装过后，可以进行一个简单的配置，点击文件，然后选择偏好设置。

![image-20200424220531333](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200424222338.png)

### 3.3.1 通用
&emsp;&emsp;在此页面，勾选==自动保存==，对写文件有很大的帮助。

### 3.3.2 外观
&emsp;&emsp;我自己的设置如下：

![image-20200424220854478](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200424222339.png)

### 3.3.3 编辑器
&emsp;&emsp;我自己的配置参考下图：

![image-20200424221008262](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200424222340.png)

### 3.3.4 图像
&emsp;&emsp;这个是我们这次的重点，依次按照图示配置

![image-20200424221423330](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200424222342.png)

&emsp;&emsp;在配置完成的时候，可以点击==验证图片上传选项==，进行测试，查看配置的 PicGo 插件是否有用。此时会出现如下界面，由于使用的是 GitHub ，因此很容易受到网速影响

![image-20200424221120889](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200424222341.png)

&emsp;&emsp;此时上传成功后，是如下界面：

![image-20200424222601453](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200424222603.png)

&emsp;&emsp;上述过程，很容易出现错误，具体可以参考文章开头借鉴的博客。==文件名已存在==这个错误，如果之前勾选打开时间戳选项，此处应该不会有这个错误。

> 本次测试，我刚开始使用的家里的 WiFi 进行上传测试，但是报错。于是我是用自己的手机热点测试上传，不久就看到 ok 啦，本篇博客的图片也是使用手机热点上传的，我也不清楚为啥 WiFi 会失败。

&emsp;&emsp;还有一个错误：Failed to fetch，这个错误参考文章经验，一般是由于端口设置错误造成的，此时需要打开 PicGo 设置，点击 ==设置 Server==，此时监听的端口号需要与 Typora 中的端口号保持一致，一般默认就是 ==36677==，只是需要去查看是否被篡改等等。

![image-20200424221841269](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200424222343.png)


### 3.3.5 Markdown
&emsp;&emsp;特别注意：<font color=#ff0000 size=3>此选项下的所有配置，在修改后，都需要重启 Typora 才能生效。</font>

&emsp;&emsp;我自己的配置如下，仅做参考

![image-20200424223241412](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200424223243.png)



![image-20200424223310237](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200424223311.png)



&emsp;&emsp;至此，Typora 软件所有的配置已经完成，有没有发现，在不知不觉间，已经实现了我们最开始的方案，使用 Typora 写作，然后利用 GitHub + PicGo 制作自己的图床，这样后续文章在移动的时候，就不怕图片丢失了！



# 4 排坑记录

&emsp;&emsp;在这里总结一下自己在使用过程中，遇到的一些坑，记录一下；

## 4.1 GitHub 成功上传图片，但是不能正常显示

&emsp;&emsp;此处好像是由于 hosts 文件解析的问题，我在使用过程中，参考的这个网址：[解决github图片不显示问题](https://blog.csdn.net/weixin_42128813/article/details/102915578)，配置后，GitHub 即可正常显示图片，很赞，已收藏文章。

&emsp;&emsp;特别提醒：<font color=#ff0000 size=3>在修改 hosts 文件之前，一定要记得先备份！备份！备份！！！避免一些未知的原因，到时候想恢复回去都很难。</font>



## 4.2 两个设备都要配置同样的环境，token 可以一样吗？

&emsp;&emsp;其实我自己在配置的时候，也是很蒙逼的，由于之前配置了一台电脑，生成了一个 token，然后第二台电脑想再次使用之前的 token 时，发现我找不到在哪了，由此推断：**GitHub 给的 token ，应该是一台设备一个**，然后我又重新生成了一个 token 给第二台电脑用。



# 5 总结

1. 整个配置过程，还是比较坎坷的， 最开始是在家里笔记本上配置，但是家里的网访问 GitHub ，很慢，就导致老是超时，不过后来尝试使用手机热点后，还ok。
2. 一步一个脚印，Go！GO！Go！