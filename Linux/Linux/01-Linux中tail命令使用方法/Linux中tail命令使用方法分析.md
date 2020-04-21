# 1 背景
&emsp;&emsp;最近在工作开发中，经常需要通过 Xshell 连接设备，进行调试等。可是在日常使用时，一般都是通过串口直接连接到控制板，查看打印信息。此时如果有另外一个人，通过 ssh 连接到控制板，他是没办法看到打印的日志信息的，当然重新启动程序，即可看到打印信息。但是在实际中不推荐这样用，因为一些设备由于条件、环境等因素限制，不能重启，那怎么办呢？

&emsp;&emsp;此时，Linux下的 tail 命令，可以帮助我们很好的解决这个问题！:smirk:

&emsp;&emsp;参考网址：[菜鸟教程 - Linux tail 命令](https://www.runoob.com/linux/linux-comm-tail.html)，看完之后，应该就有一个大概的了解了。

> 顺便附上菜鸟教程Linux命令大全的网址：[菜鸟教程 - Linux命令大全](https://www.runoob.com/linux/linux-command-manual.html)，温馨提示：善于使用 Ctrl + F 快捷键哦:wink:

&emsp;&emsp;下边是自己在使用过程中的，经验总结记录。

# 2 tail 命令分析
&emsp;&emsp;tail 命令可用于查看文件的内容。英文翻译：==尾==。在实际使用时，常用的一个命令如下：
```shell
tail -f filename
```

&emsp;&emsp;此命令使用了一个主要的参数 -f，可以用来查阅==正在改变的日志文件==。

&emsp;&emsp;此命令会把 filename 文件里的最尾部的内容显示在屏幕上，并且不断刷新，只要 filename 更新就可以看到最新的文件内容。

&emsp;&emsp;命令格式：
```shell
tail [参数] [文件名]
```

## 2.1 参数分析
&emsp;&emsp;tail 命令可以搭配多个参数使用，不过我目前只用到了 -f，参考菜鸟教程总结常用参数如下：
| 参数 | 作用 |
|:---:|:---|
| -f | 循环读取 |
| -q | 不显示处理信息 |
| -v | 显示详细的处理信息 |
| -c<数目> | -c + 空格 + 数目 n：显示的字节数。<br/>自己测试是从文件末尾开始往前计数 n 个字节数。 |
| -n<行数> | -n + 空格 + 行数 n：显示文件的尾部 n 行内容。 |
| --pid=PID | 一般与 -f 一块使用，表示在进程 ID、PID 死掉之后结束 |

## 2.2 简要举例
 - 实时打印日志文件
```shell
tail -f log.log
```

 - 显示文件 log.log 的内容，从第20行至文件末尾
```shell
tail +20 log.log
```

 - 显示文件 log.log 的最后100个字符
```shell
tail -c 100 log.log
```

 - 显示文件 log.log 最后100行数据
```shell
tail -n 100 log.log
```

 - 除了 log.log 前99行不显示外，显示第100行到末尾行
```shell
tail -n -100 log.log
```

 - 实时打印非当前路径的日志文件 log.log
```shell
tail -f /etc/log.log
```

# 3 重定向实时打印
&emsp;&emsp;当我们在实际使用时，可能会同时有多个进程在运行，那这每个进程都会有日志信息打印，当日志文件太多，设备空间不够时，怎么办？怎么能只看某个正在运行的进程打印出来的日志信息呢？那就要使用重定向命令了

&emsp;&emsp;参考网址：[LINUX 下使用 reredirect 重定向进程输出](https://blog.csdn.net/horotororensu/article/details/104505768)

&emsp;&emsp;上述网址有对应的安装路径，以及编译的时候，需要配置相关参数，由于我只是在实际使用过程中，已经有这个东西了，所以我也就没有太深入的了解怎么安装等等。

&emsp;&emsp;具体用法：

 - 先使用命令查看当前进程ID
```shell
ps -aux                    // 全部显示
ps -aux | grep 进程名       // 只显示与“进程名”相关的进程信息，增加一层过滤
```
 - 重定向到指定进程ID（PID）
```shell
reredirect -m filename 进程ID   // 将此进程的日志信息，定向输出到 filename 此文件中。
```
 - 实时查看日志信息
```shell
tail -f filename
```
