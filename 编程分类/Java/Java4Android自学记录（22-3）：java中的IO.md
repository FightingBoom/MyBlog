> 道阻且长，行则将至。埋头苦干，不鸣则已，一鸣惊人！加油，骚年！

# 目录及资源索引

&emsp;&emsp;[Java4Android自学过程目录及资源索引](https://blog.csdn.net/Fighting_Boom/article/details/103850497)

# 1 处理流使用实例

&emsp;&emsp;参考老师课件，具体解释内容如下图：

![image-20200530141430426](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200530163543.png)

&emsp;&emsp;全称：字符输入处理流；使用这个类的时候，大部分都是为了使用其中这个方法：如上图所示，读取一行。

&emsp;&emsp;比如有一个类似这样的文件需要处理，每一行都是一个用户的信息

```shell
张三 F 20
李四 M 21
王五 F 22
赵六 M 23
```

&emsp;&emsp;这个时候，读取这个文件怎样最方便？当然是一次读取一行；这样就可以利用上述函数；

&emsp;&emsp;那么具体的使用方法是怎么样的呢？生成方法，接收的是一个 Reader 类的对象，下边用代码实验如下：

```java
import java.io.*;

class Test 
{
	public static void main(String args[])
	{
		FileReader fileReader = null;
		BufferedReader bufferedReader = null;
		
		try
		{
			fileReader = new FileReader("users.txt");
			bufferedReader = new BufferedReader(fileReader);
			
			String line = bufferedReader.readLine();
			System.out.println(line);
		}
		catch(Exception e)
		{
			System.out.println(e);
		}
		finally
		{
			try
			{
				fileReader.close();
				bufferedReader.close();
			}
			catch(Exception e)
			{
				System.out.println(e);
			}
		}		
	}
}
```

&emsp;&emsp;上述代码，编译运行后结果如下：

![image-20200530143257015](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200530163700.png)

&emsp;&emsp;可以看到第一次出现了乱码，即使之前是加上了编译所使用的字符集，还是不可以。后来发现，

1. 第一次出现乱码，users.txt 文本的编码为 UTF-8 编码；
2. 第二次正常显示，是此文本编码修改为 ANSI 后，恢复正常;
3. 具体原因暂时未知。



&emsp;&emsp;如何把这几行内容，全部打印出来呢？修改部分代码如下，我们只需要增加一个 while 循环即可

```java
import java.io.*;

class Test 
{
	public static void main(String args[])
	{
		FileReader fileReader = null;
		BufferedReader bufferedReader = null;
		
		try
		{
			fileReader = new FileReader("users.txt");
			bufferedReader = new BufferedReader(fileReader);
			
			String line = null;
			while(true)
			{
				line = bufferedReader.readLine();
				if(null == line)
				{
					break;
				}
				System.out.println(line);
			}				
		}
		catch(Exception e)
		{
			System.out.println(e);
		}
		finally
		{
			try
			{
				fileReader.close();
				bufferedReader.close();
			}
			catch(Exception e)
			{
				System.out.println(e);
			}
		}		
	}
}
```

&emsp;&emsp;上述代码，编译运行后的结果如下：

![image-20200530143602265](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200530163713.png)

&emsp;&emsp;这个函数什么时候返回 NULL 呢？当读到末尾的时候，就返回 NULL ；

&emsp;&emsp;上述就是所谓的处理流，凡是要使用处理流的，都必须首先有一个节点流。

# 2 “装饰者（Decorator）”模式

## 2.1 示例演示

&emsp;&emsp;老师举了一个例子，先来一步一步深入，具体如下：

![image-20200530145322431](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200530145322.png)

&emsp;&emsp;疑问：当工人的类别，及工人所属的公司，越来越多时，怎么办呢？

&emsp;&emsp;此时可以先定义一个 Worker 的接口，代码如下：

```java
interface Worker
{
	public void doSomeWork();
}
```

&emsp;&emsp;接着定义一个修水管的类，Plumber，此类继承 Worker 接口，需要实现父类中的函数，具体代码如下：

```java
class Plumber implements Worker
{
	public void doSomeWork()
	{
		System.out.println("修水管");
	}
}
```

&emsp;&emsp;接着定义一个木工类，修门窗的，Carpenter，同样继承 Worker 接口，需要实现父类中的函数，具体代码如下：

```java
class Carpenter implements Worker
{
	public void doSomeWork()
	{
		System.out.println("修门窗");
	}
}
```

&emsp;&emsp;然后定义一个子类 AWorker，继承 Worker ，相当于是 A 公司的员工，同样需要实现父类中的函数，还需要加上一个构造函数（参数类型为父类 Worker），此时代码如下：

```java
class AWorker implements Worker
{
	private Worker worker;
	
	public AWorker(Worker worker)
	{
		this.worker = worker;
	}
	
	public void doSomeWork()
	{
		System.out.println("你好");
		worker.doSomeWork();
	}
}
```

&emsp;&emsp;最后定义一个有主函数的类，生成一个 A 公司修水管的工人，此时需要向上转型，具体代码如下：

```java
class Test01
{
	public static void main(String args[])
	{
		// 生成一个A公司水管工对象
		Plumber plumber = new Plumber();
		AWorker aWorker = new AWorker(plumber);	// 向上转型
		aWorker.doSomeWork();
	}
}
```

&emsp;&emsp;最后代码编译运行结果如下：

![image-20200530151406311](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200530151406.png)

&emsp;&emsp;分析一下，在 AWorker 中有一个 Worker 的引用，其实这是一个面向对象的思想，不使用继承，而是在 A 公司这个类中，有 Worker 的一个成员变量；好处是什么呢？==通用性==；假如此时要生成一个 A 公司的木匠工，此时就可以使用这个通用的类，只是传进去的参数类型为木匠工向上转型后的类型。

&emsp;&emsp;上代码看一下，就一目了然了，如下：

```java
class Test01
{
	public static void main(String args[])
	{
		// 生成一个A公司水管工对象
		Plumber plumber = new Plumber();
		AWorker aWorker = new AWorker(plumber);	// 向上转型
		aWorker.doSomeWork();
		
		Carpenter carpenter = new Carpenter();
		AWorker aWorker2 = new AWorker(carpenter);
		aWorker2.doSomeWork();
	}
}
```

&emsp;&emsp;上述代码，编译运行后，结果如下，可以看到木匠的修门窗，也打印出来了。

![image-20200530152401100](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200530152401.png)



## 2.2 示例分析

&emsp;&emsp;上述示例，已经演示完毕，那么我的疑问来了，感觉有很多不理解的地方，比如：

1. 为什么要这么设计？好处是什么？
2. 目前看来定义了很多类，感觉很复杂呀，可是我目前不需要这么复杂、这么多的类，就能实现功能了呀？



&emsp;&emsp;别慌，我们仔细理解，分析一下就很容易得出结论，面向对象编程的终极目标是什么？消除程序中的重复代码；好了，这就让我们来解答之前的问题：

1. 这样设计，便于后续扩展，便于消除重复代码！
2. 不要被目前的需求局限了思维，目前只是举这么简单一个例子，如果我们写出来一个程序，后续随着用户量增加，产品需求增加，需要改变时，还要重构一遍代码，那就很麻烦了。就像天宫一号空间站一样，每次送上去的肯定是留有一个或多个对接下次设备的接口，如果你直接就封死了，后续再要发射设备，怎么办？？？哈哈，道理就是这么个样子。



&emsp;&emsp;**那么先消除上边这些疑问，再来分析一下这样写的意义，个人感觉的有如下几个方面**

1. 虽然刚开始看起来要定义很多类，很复杂，但其实不然；
2. 把共同的部分，一层一层的抽出来，比如最抽象的，大家都是工人；其次再分水管工、木匠工；接着可以再分 A 公司的水管工、木匠工，B 公司的水管工、木匠工；等等
3. 这样把公共的抽出来，最抽象的就可以作为父类，就像大家交流的一个通道似的；举个例子，我在深圳，就是深圳人，你在郑州就是郑州人；深圳是广东省的，郑州是河南省的；而广东又是中国的，河南也是中国的，你看，我们俩的联系/共同点不就出来了吗？这样我们对外，就可以一致的说，我是中国人！
4. 在进一步的分析，你在河南省new出一个对象，我在广东省new出来一个对象；这样你的就是中国河南省的对象，我的就是中国广东省的对象，哈哈哈哈；



# 3 总结

1. 上述示例，都是自己根据自己的理解想象出来的，如果有误，还望多多指教~
2. 装饰者模式：把类似 AWorker 这种类称为装饰者，把木匠等称为被装饰者；
3. 压缩流，实现压缩和解压缩文件；
4. 装饰者模式，理解还不够深入，后续有时间，要进一步深入了解一下，或者结合实践，多多练习！加油啦~

> 如果文章内容有误，麻烦评论/私信多多指教，谢谢！如果觉得文章内容还不错，留个赞呗，您的点赞就是对我最大的鼓励，谢谢您嘞！