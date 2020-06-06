> 道阻且长，行则将至。埋头苦干，不鸣则已，一鸣惊人！加油，骚年！

# 目录及资源索引

&emsp;&emsp;[Java4Android自学过程目录及资源索引](https://blog.csdn.net/Fighting_Boom/article/details/103850497)

# 1 多进程与多线程

&emsp;&emsp;简单地说，多进程：在操作系统中能（同时）运行多个任务（程序）；多线程：在同一应用程序中有多个顺序流（同时）执行。

&emsp;&emsp;每启动一个应用，就是启动一个进程。对于 Android ，原则上来讲，一个软件只有一个进程。



# 2 线程的执行过程

&emsp;&emsp;参考老师课件，有如下示例，类似一个抽水机，两条水管同时在抽水；

![image-20200603234624792](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200603234652.png)

## 2.1 线程执行流程图

&emsp;&emsp;线程的整个执行过程，简要总结一下就是：创建一个新线程 -> 启动线程 -> 线程运行（受控调度） -> 运行完毕 -> 线程释放/回收；

&emsp;&emsp;参考老师图片，总结如下：

![image-20200604224125486](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200604224125.png)

&emsp;&emsp;针对上图，再次理解线程执行过程：先创建线程，然后开始运行，然后进入就绪状态，接着进入运行状态，然后等待 CPU 调度，进入阻塞，然后解除阻塞，接着运行，等等，直到运行完毕，销毁线程。



# 3 创建线程的方法

## 3.1 方法一：继承类 Thread

&emsp;&emsp;定义一个线程类，继承类 Thread ，并且重写其中的方法 run() ，方法 run() 称为线程体；

&emsp;&emsp;注意：<font color=#ff0000 size=4>由于 java 只支持单继承，用这种方法定义的类不能再继承其他类。</font>

&emsp;&emsp;具体实现方法呢，看下边代码

```java
class FirstThread extends Thread
{
	public void run()
	{
		for(int i = 0; i < 100; i++)
		{
			System.out.println("FirstThread-->" + i);
		}
	}
}
```

&emsp;&emsp;再新建一个主函数类，具体代码如下：

```java
class Test
{
	public static void main(String args[])
	{
		// 生成线程类的对象
		FirstThread ft = new FirstThread();
		
		// 启动线程
		ft.start();
	}
}
```

&emsp;&emsp;上述代码，与我们一开始的思路都保持一致，主函数中的内容也很简单，new 一个对象，然后启动线程，就完事儿了。

&emsp;&emsp;那么上述代码运行过程是怎么样的呢？

![image-20200604225247490](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200606093912.png)

&emsp;&emsp;上边只是截图下来一部分的内容，由于使用了 for 循环，因此他会一直走完所有步骤。

&emsp;&emsp;那么问题就来了，猜猜此时几个线程正在运行？没错，答案就是 2 个，因为 main 函数本身也是一个线程，我们称之为主线程。那么怎么验证一下我们的结论呢？在主函数中在新增一些打印就好了，如下：

```java
class Test
{
	public static void main(String args[])
	{
		// 生成线程类的对象
		FirstThread ft = new FirstThread();
		
		// 启动线程
		ft.start();
		
		for(int i = 0; i < 100; i++)
		{
			System.out.println("main-->" + i);
		}
	}
}
```

&emsp;&emsp;程序编译后的运行结果如下，会发现这两个线程是在交替运行的

![image-20200604231406010](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200606094318.png)

&emsp;&emsp;此时问题又来了，我们不是常说线程是可以同时运行的吗？注意啦，此时所说的 “同步” ，是从宏观层面来说，比如运行一次 A 或 B 需要 1ms ，如果在 1 个小时内，A B 依次交替运行，也就是 A 在这段时间内运行 30 分钟，B 也运行30分钟， 如果把比例尺放大，从远处看，就可以说 A B 是在同时运行；但是，如果把比例尺缩小，从近处看，确实 A B 不是在同步运行，也就是微观看到的 A 先运行 1ms ，B 再运行 1ms ，依次交替运行。

&emsp;&emsp;注意：<font color=#ff0000 size=4>如果不使用 ft.start() ，直接使用 ft.run()，则就是在一个线程内运行程序，不是多线程。</font>

## 3.2 方法二：实现接口 Runnable

&emsp;&emsp;提供一个实现接口 Runnable 的类作为线程的目标对象，在初始化一个 Thread 类或者 Thread 子类的线程对象时，把目标对象传递给这个线程实例，由该目标对象提供线程体。

&emsp;&emsp;注意此时我们继承的是一个 **接口** ，代码如下：

```java
class RunnableImpl implements Runnable
{
	public void run()
	{
		for(int i = 0; i < 100; i++)
		{
			System.out.println("Runnable-->" + i);
		}
	}
}
```

&emsp;&emsp;&emsp;主函数代码如下：

```java
class Test
{
	public static void main(String args[])
	{
		// 生成一个 Runnable 接口实现类的对象
		RunnableImpl ri = new RunnableImpl();
		
		// 生成一个Thread对象，并将Runnable接口实现类的对象作为
		// 参数传递给该Thread对象（参数为Runnable类型的）
		Thread t = new Thread(ri);
		
		// 通知Thread对象，执行start方法
		t.start();
	}
}
```

&emsp;&emsp;上述代码，编译后运行结果如下：

![image-20200606094834697](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200606094957.png)



## 3.3 总结两种方法

&emsp;&emsp;第一种是继承 Thread 类；第二种是实现 Runnable 接口；

&emsp;&emsp;在实际使用中，对继承能不用就不用，因为 java 只能支持单继承，因此还是实现接口比较好。



# 4 总结

1. 简单了解 java 中创建线程的两种方法，以及各自的优劣点；
2. 实际使用基本代码进行练习，但是还不够深入；
3. 后续需要深入了解，把基础打牢；



> 如果文章内容有误，麻烦评论/私信多多指教，谢谢！如果觉得文章内容还不错，留个赞呗，您的点赞就是对我最大的鼓励，谢谢您嘞！