> 道阻且长，行则将至。埋头苦干，不鸣则已，一鸣惊人！加油，骚年！

# 目录及资源索引
&emsp;&emsp;[Java4Android自学过程目录及资源索引](https://blog.csdn.net/Fighting_Boom/article/details/103850497)
# 1 什么是I/O？

&emsp;&emsp;从字面意思理解也很简单，其实就是输入（input）输出（output）首字母的缩写。CPU 与外部设备、存储器的连接和数据交换都需要通过接口设备来实现，前者称为 I/O 接口，而后者则称为存储器接口。

&emsp;&emsp;I/O 设备品种繁多，相应的接口电路也各不相同，因此，我们习惯上说的接口，只是指 I/O 接口。


&emsp;&emsp;Java 中的 I/O 操作是通过输入/输出**数据流**的形式来完成的，因此它也称作**数据流操作**。通俗地讲，这实际上就是一种数据的输入输出方式。

&emsp;&emsp;I/O 操作的目标：从数据源当中读取数据，以及将数据写入到数据目的地当中。



# 2 I/O的流向

&emsp;&emsp;既然 I/O 操作实际是数据的输入输出方式，那就肯定涉及到一个方向问题，需要一个参照物，并且流向的意义很重要。

- 输入：将数据源读取到程序中，就是输入；
- 输出：需要将程序中的内容，写入到网络，其他文件等，就是输出；



> 问：输入输出为什么叫流？
>
> 答：stream 有流动的意思，可以把流看成一个管道，所谓流，就是在数据源与程序之间建立一个数据流淌的管道，数据不是一下就全到程序中去，而是需要慢慢的传输；



# 3 I/O的分类
&emsp;&emsp;按照老师的讲解，大致有三种分类方法

- 第一种分法

	1. 输入流；
	2. 输出流

- 第二种分法

	1. 字节流
	2. 字符流

- 第三种分法

	1. 节点流
	2. 处理流
	
	

&emsp;&emsp;字节流：以字节为基础；

&emsp;&emsp;字符流：是以字符为基础；每次读写，都是一个或者几个字符；



&emsp;&emsp;节点流：真正处理数据的I/O流；

&emsp;&emsp;处理流：在节点流基础上对数据再加工。（例如：水管外，加热，磁化等）



&emsp;&emsp;<font color=#ff0000 size=4>本节主要学习字节流</font>

# 4 字节流的核心类

&emsp;&emsp;<font color=#ff0000 size=3> `InputStream` </font>与<font color=#ff0000 size=3> `OutputStream` </font>是所有的 **字节流** 的父类；即所有的字节流都是这两个的子类。

&emsp;&emsp;核心类提供的核心方法如下：
```java
// InputStream
int read(byte[] b, int off, int len)

// OutputStream
void write(byte[] b, int off, itn len)
```

&emsp;&emsp;我刚开始不是学 Java 的，看到<font color=#ff0000 size=3> `byte[] b` </font>这种形式，很是懵逼，后来查了一下发现，只是写法不太一样，最终效果还是一样的，就是定义了一个类型为 **byte** 的数组名为 **b** 的数组，大小不确定，而已......，要是按照 C/C++ 中的写法，应该是<font color=#ff0000 size=3> `byte b[]` </font>，其实没啥差别。。。

&emsp;&emsp;先说输入流的 **read** 函数
 - **byte[] b**：就是一个 byte 类型的数组；
 - **off**：偏移量，就是从数组的第几位开始写；
 - **len**：读取一次，最多读多少数据；（感觉跟喝一杯水一样，一口最多喝多少...）
 - **返回值**：这次总共读取了多少个数据

&emsp;&emsp;然后是输出流的 **write** 函数
 - **byte[] b**：要写进去的数据；
 - **off**：偏移量，从 byte 数组的第 off 位开始，往后的才写到文件中去，前边的不要了；
 - **len**：这一次总共要往文件中写入多少个数据；

&emsp;&emsp;实际演示代码如下：
```java
import java.io.*;	// 导入类

class Test 
{
	public static void main(String args[])
	{
		FileInputStream fis = null;
		
		try
		{
			fis = new FileInputStream("from.txt");
			byte [] buffer = new byte[100];
			fis.read(buffer, 0, buffer.length);
			
			for(int i = 0; i < buffer.length; i++)
			{
				System.out.println(buffer[i]);
			}
		}
		catch(Exception e)
		{
			System.out.println(e);
		}
		
	}
}
```
&emsp;&emsp;其中 **from.txt** 中的内容为 **abcd** ，则上述代码运行后的结果如下：

![image-20200524150143551](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200524151939.png)

&emsp;&emsp;由上述运行结果可以看到，把 **abcd** 这几个字母的 ASCII 码全部打印出来了，后边没有的默认填0，为什么呢？因为 **buffer.length** 是数组的长度，也就是我一次能读100个，结果你只给我4个，那剩下96个就默认填写0了。

&emsp;&emsp;如果要测试一下偏移量，也就是不想从 **buffer** 开头开始写，那么修改一下 **off** 即可（假设偏移量为5），有改动的部分如下：

```java
fis.read(buffer, 5, buffer.length - 5);

for(int i = 0; i < buffer.length - 5; i++)
{
    System.out.println(buffer[i]);
}
```

&emsp;&emsp;此时再次运行代码，可以看到如下效果，会发现，前5个字符，变成0了，从第6个字符开始写。

![image-20200524145811170](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200524151929.png)

&emsp;&emsp;又有问题啦，我的文件中是一个字符串，这个地方为啥是 ASCII 码？这是由于我们的数组类型决定的，读取出来变成 **byte** 类型了，想要还原为字符，加上一个转换即可

```java
String s = new String(buffer);

System.out.println(s);
```

&emsp;&emsp;此时再看打印内容，就会发现恢复正常了

![image-20200524145201365](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200524151938.png)



# 5 字节流的使用

&emsp;&emsp;问题：我们需要把 **from** 文件的内容，通过字节流的方式，复制到 **to** 文件中，应该如何去做？

&emsp;&emsp;解答：之前关于字节流的使用，已经学会了如何读取文件，那同样的，我们把读取到的文件，使用对应的函数写入到目的文件，不就可以了吗？尝试代码如下：

```java
import java.io.*;	// 导入类

class Test 
{
	public static void main(String args[])
	{
		// 声明输入流引用
		FileInputStream fis = null;
		
		// 声明输出流的引用
		FileOutputStream fos = null;
		
		try
		{
			// 生成代表输入流的对象
			fis = new FileInputStream("from.txt");
			
			// 生成代表输出流的对象
			fos = new FileOutputStream("to.txt");
			
			// 生成一个字节数组
			byte [] buffer = new byte[100];
			
			// 调用输入流对象的read方法，读取数据
			int temp = fis.read(buffer, 0, buffer.length);
			
			// 读出来多少数据，就写进去多少数据
			fos.write(buffer, 0, temp);
		}
		catch(Exception e)
		{
			System.out.println(e);
		}
		
	}
}
```

&emsp;&emsp;上述代码的运行结果，如果我们没有打印的话，在终端上是看不到任何变化的， 不过我们能看到目的文件 **to** 中，有内容了，大小也变了。

&emsp;&emsp;分析一下上边的代码，其实就多了三条语句，一条是声明输出流的引用；一条是生成代表输出流的对象；还有一条是写函数，这就完成了我们想要的操作。

> <font color=#ff0000 size=4>温馨提示：要好好利用 read 的返回值，是读到了多长的数据，如果不用这个，而直接用数组的总长度，则写到文件中的，在数据不够这个总长度的情况下就会有很多 null。</font>



# 6 总结

1. I/O系统的主要目标是为了对数据进行读写操作；

2. 数据的流向以Java程序为参照物；

3. I/O流可以有三种分类方法；

4. read 方法和 write 方法；



> 如果文章内容有误，麻烦评论/私信多多指教，谢谢！如果觉得文章内容还不错，留个赞呗，您的点赞就是对我最大的鼓励，谢谢您嘞！