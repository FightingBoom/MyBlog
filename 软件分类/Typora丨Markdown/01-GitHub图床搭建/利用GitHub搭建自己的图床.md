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






