> 道阻且长，行则将至。埋头苦干，不鸣则已，一鸣惊人！加油，骚年！

# 目录及资源索引
&emsp;&emsp;[Java4Android自学过程目录及资源索引](https://blog.csdn.net/Fighting_Boom/article/details/103850497)

# 1 多线程数据安全
&emsp;&emsp;如果两个线程同时运行，他们需要对同一块数据操作，而此时我们如果不加以控制，就会出现 “打架” 的现象，可以看一个代码示例
```java
class MyThread implements Runnable
{
	int i = 100;
	
	public void run()
	{
		while(true)
		{
			System.out.println(Thread.currentThread().getName() + i);
			
			i--;
			
			Thread.yield();
			if(i < 0)
			{
				break;
			}
		}
	}
}
```
&emsp;&emsp;分析一下此类中的代码：

 - **Thread.currentThread**：这个是 Thread 类的一个静态方法，用来获取当前线程；
 - **getName**：可以获取当前线程名字；
 - **yield**：让出CPU，让线程重新抢占CPU；


&emsp;&emsp;此时我们再创建另外一个主函数，具体代码如下
```java
class Test 
{
	public static void main(String args[])
	{
		MyThread myThread = new MyThread();
		
		Thread t1 = new Thread(myThread);
		Thread t2 = new Thread(myThread);
		
		t1.setName("线程a");
		t2.setName("线程b");
		
		t1.start();
		t2.start();

	}
}
```
&emsp;&emsp;此时我们生成了两个 Thread 对象，但是这两个 Thread 对象共用一个线程体；

&emsp;&emsp;但是每一个线程都有名字，可以通过 Thread 对象的<font color=#ff0000 size=3>` setName() `</font>方法设置线程名字，也可以使用<font color=#ff0000 size=3>` getName() `</font>方法获取线程名字；

&emsp;&emsp;接下来就是分别使用<font color=#ff0000 size=3>` start() `</font>方法启动线程；

&emsp;&emsp;此时编译上述代码后，运行结果如下，此执行过程是参考老师的截图，自己尝试几次没试出来此结果，因此借用老师图片加以说明。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200607152751694.png)

&emsp;&emsp;由上述执行过程可以看到，没有出现与 **1** 相关的打印，为什么会这样呢？

&emsp;&emsp;原因为：线程同步错误，就是多个线程共用同一份数据，就可能导致这样的错误。

> 举个小例子：就像桌子上有一个苹果，我和你都准备去拿，此时如果没有顺序，我们俩共同去操作，就极有可能出现苹果掉地上了，我们俩都没有拿到苹果。

&emsp;&emsp;怎么解决这个问题呢？**同步代码块**

# 2 同步代码块
&emsp;&emsp;同步代码块主要是用此函数来实现：<font color=#ff0000 size=3>` synchronized `</font>，实际实现代码效果如下：
```java
class MyThread implements Runnable
{
	int i = 100;
	
	public void run()
	{
		while(true)
		{
			synchronized(this)	// 同步代码块
			{
				System.out.println(Thread.currentThread().getName() + i);
				
				i--;
				
				Thread.yield();
				if(i < 0)
				{
					break;
				}
			}	
		}
	}
}
```
&emsp;&emsp;个人感觉同步代码块的作用可以类比 Linux 中的线程同步锁，在一个线程执行代码的时候，不会有另外一个线程来执行此代码块；

&emsp;&emsp;但拿到锁的不代表会一次把下边代码执行完，线程还是会被抢占的，只不过如果b没拿到锁，就需要**阻塞**等待；

> 再举一个小例子：还是之前那个苹果，如果此时加了锁，我先去对这个苹果进行操作，比如咬一口，此时我还没吃完，还没把苹果放到原位离开，你此时就算来了，也只能在旁边看着我吃，直到我把苹果放下离开之后，你才能拿得到这个苹果，然后对这个苹果做一些事情。哈哈

# 3 总结
1. 初步认识与线程安全有关的问题；
2. 通过老师的实例，进一步熟悉；
3. 简单了解最基本的处理线程打架的方法；
4. 每天进步一点点，革命尚未成功，同志仍需努力！:muscle::muscle::muscle:


> 如果文章内容有误，麻烦评论/私信多多指教，谢谢！如果觉得文章内容还不错，留个赞呗，您的点赞就是对我最大的鼓励，谢谢您嘞！