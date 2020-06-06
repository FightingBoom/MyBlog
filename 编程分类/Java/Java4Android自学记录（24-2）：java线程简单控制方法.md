> 道阻且长，行则将至。埋头苦干，不鸣则已，一鸣惊人！加油，骚年！



# 目录及资源索引

&emsp;&emsp;[Java4Android自学过程目录及资源索引](https://blog.csdn.net/Fighting_Boom/article/details/103850497)



# 1 线程的简单控制方法

## 1.1 sleep 函数

&emsp;&emsp;字面意思很简单，就是睡眠，结合本文就是让线程休息一会，跟我们裸机开发常说的**延时**有点像。

&emsp;&emsp;需要注意的是，sleep （结束）之后，不是立马就进入运行状态，而是进入就绪状态，此时就和其他线程在同一起跑线，等待抢占CPU。

&emsp;&emsp;==为什么这样做呢？因为有的时候我们需要让当前正在执行的线程暂停一段时间，并且进入阻塞状态，就会用到此方法。==

&emsp;&emsp;我们尝试修改之前例程的代码，增加 sleep 函数如下：

```java
class RunnableImpl implements Runnable
{
	public void run()
	{
		for(int i = 0; i < 100; i++)
		{
			System.out.println("Runnable-->" + i);
			if(50 == i)
			{
				try
				{
					Thread.sleep(2000);
				}
				catch(Exception e)
				{
					System.out.println(e);
				}
			}
		}
	}
}
```

&emsp;&emsp;上述代码，编译运行后的结果，对比之前的运行结果，会发现在打印出 **50** 之后，程序会停止 2s ，然后继续运行。此时如果在主线程中有打印的话，是不受此 **“延时”** 影响的。

> 如果当前线程调用 sleep() 方法进入阻塞状态，那么在其睡眠时间段内该线程不会获得执行机会，即使系统中没有其他可运行的线程，处于睡眠中的线程也不会运行，因此 sleep() 方法常用来暂停程序的执行。



## 1.2 yield 函数

&emsp;&emsp;使用此函数，此线程会让出 CPU。让出之后，还是这么多线程在一块抢，但不代表此线程不会去抢 CPU。通俗一点讲就跟 ***复位*** 差不多，哪一个线程使用这个函数，就回到起点，等待与其他线程一块赛跑（一块抢占 CPU）。

&emsp;&emsp;使用 yield() 方法，可以让当前正在执行的线程暂停，但它不会阻塞该线程，只是将该线程转入就绪状态。此方法只是让当前线程暂停一下，让系统的线程调度器重新调度。完全可能的情况是：**当某个线程调用 yield() 方法暂停之后，线程调度器又将其调度出来重新执行。**

&emsp;&emsp;实际上当某个线程调用 yield() 方法暂停之后，只有优先级与当前线程相同，或者比当前线程更高的处于就绪状态的线程才会获得执行机会。



## 1.3 设置线程优先级

&emsp;&emsp;线程的优先级用数字表示，范围为 1 ~ 10，与线程优先级相关的方法如下

- **查看线程优先级**

```java
t.getPriority();		// 查看线程优先级
```

- **设置线程优先级**

```java
t.setPriority();		// 设置线程优先级
```

- **线程优先级相关宏定义**

```java
public final static int MIN_PRIORITY = 1;	// 最小优先级

public final static int NORM_PRIORITY = 5;	// 默认优先级

public final static int MAX_PRIORITY = 10;	// 最大优先级
```

&emsp;&emsp;首先可以使用函数查看当前线程优先级，具体代码如下：

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
		
		System.out.println(t.getPriority());
		
		// 通知Thread对象，执行start方法
		t.start();
	}
}
```

&emsp;&emsp;上述代码编译后运行结果如下，可以看到如果没有设置优先级的话，默认为 5。

![image-20200606204055845](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200606210100.png)

&emsp;&emsp;同样的，我们也可以给线程设置为最大优先级

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
				
		t.setPriority(Thread.MAX_PRIORITY);
				
		// 通知Thread对象，执行start方法
		t.start();
		
		System.out.println(t.getPriority());
	}
}
```

&emsp;&emsp;编译后运行结果如下：

![image-20200606204221108](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200606210109.png)

&emsp;&emsp;再次尝试给线程设置最小优先级，其实只是使用不同的变量而已，代码如下：

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
				
		t.setPriority(Thread.MIN_PRIORITY);	// 设置最小优先级
				
		// 通知Thread对象，执行start方法
		t.start();
		
		System.out.println(t.getPriority());
	}
}
```

&emsp;&emsp;编译后运行结果如下：

![image-20200606204351190](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200606210115.png)



&emsp;&emsp;简单总结一下：线程优先级范围为 1 ~ 10，最小优先级为 1 ，最大为 10 ，默认为 5 ，可以直接使用 Thread 所提供的静态常量来设置线程的优先级。

&emsp;&emsp;<font color=#ff0000 size=4>注意：优先级越高的线程，执行的**概率**就越大，而不是一定就是他先执行；线程能不能运行，关键还是看他能不能抢到 CPU 。</font>



# 2 小插曲

&emsp;&emsp;在看书的过程中，书上的最大优先级是 1 ，我是懵逼的，后来去请教了一下，果然是书本上的弄错了。

&emsp;&emsp;这个是书本上的定义

![3c734d3e7d41ea0fd22ad568bd4e2ef](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200606205229.png)

&emsp;&emsp;这个是我参考别人的方法，也去找了一下 **JDK** 中的源码，发现还真是书本上的错了，唉，心累

![44281f4f31ba359aaaab23e57a52d3d](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200606205510.png)



# 3 总结

1. 基本了解了线程控制的方法：睡眠线程（sleep），线程让步（yield），获取线程优先级，设置线程优先级等；
2. 整体来说还是遇到了一些问题，踩了一些坑，不过还好啦，慢慢排坑就是啦；
3. 每天进步一点点，革命尚未成功，同志仍需努力！:muscle::muscle::muscle:



> 如果文章内容有误，麻烦评论/私信多多指教，谢谢！如果觉得文章内容还不错，留个赞呗，您的点赞就是对我最大的鼓励，谢谢您嘞！