> 道阻且长，行则将至。埋头苦干，不鸣则已，一鸣惊人！加油，骚年！

# 目录及资源索引

&emsp;&emsp;[Java4Android自学过程目录及资源索引](https://blog.csdn.net/Fighting_Boom/article/details/103850497)



# 1 大文件的读写方法

&emsp;&emsp;实际中使用 read 方法可以把读取到的数据放到 buffer 中；目前字节流，数组长度都是固定的，不过无论长度为多少，我们在写/读的时候，都有个尽头。这样我们就可以一点一点读取，需要用到循环来读取，类似之前学的 C++ 的环形缓冲区。



&emsp;&emsp;字节换算方法再次熟悉如下：

```java
1G = 1024M = 1024 * 1024 K = 1024 * 1024 * 1024 B
```



&emsp;&emsp;循环思路：每读取一次，都会返回读到多少个字节；最后一次，读取数据已经读完了，那 read 方法会返回一个什么值？当数据读取完之后，会返回 -1 ；

&emsp;&emsp;那么此时我们就可以定义一个循环，当返回值为 -1 时，就停止，否则就一直执行。



&emsp;&emsp;话不多说，上代码

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
			byte [] buffer = new byte[1024];
			while(true)
			{
				// 调用输入流对象的read方法，读取数据
				int temp = fis.read(buffer, 0, buffer.length);
				if(-1 == temp)
				{
					break;	// 如果读取完毕，就跳出
				}
				
				// 读出来多少数据，就写进去多少数据
				fos.write(buffer, 0, temp);				
				
			}
			
			// 把数组内的数据，还原为字符
			// String s = new String(buffer);
			
			// 将会去除掉这个字符串的首尾空格和空字符
			// s = s.trim();
			
			// System.out.println(s);
		}
		catch(Exception e)
		{
			System.out.println(e);
		}
		
	}
}
```



&emsp;&emsp;上述程序编译后，运行结果如下：

![image-20200530122337884](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200530124219.png)



&emsp;&emsp;运行后，什么结果都没有，不过这是因为我们没有加打印，此时没有结果就是最好的结果，我们去看文件夹中的内容：
![image-20200530122437465](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200530124220.png)



&emsp;&emsp;不过此时上述代码还是不完整的，不知道你有没有发现，我们在打开文件，使用完毕之后，没有关闭文件的相关操作，此时操作肯定是有漏洞的，参考我们之前的经验，应该在 finally 中，加上关闭文件的操作，这样的好处是，总是能执行到关闭文件这一步操作，修改后的代码如下：

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
			byte [] buffer = new byte[1024];
			while(true)
			{
				// 调用输入流对象的read方法，读取数据
				int temp = fis.read(buffer, 0, buffer.length);
				if(-1 == temp)
				{
					break;	// 如果读取完毕，就跳出
				}
				
				// 读出来多少数据，就写进去多少数据
				fos.write(buffer, 0, temp);				
				
			}
		}
		catch(Exception e)
		{
			System.out.println(e);
		}
		finally
		{
			fis.close();
			fos.close();
		}
	}
}
```

&emsp;&emsp;此时编译运行一下，结果如下：

![image-20200530122913138](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200530124221.png)

&emsp;&emsp;我们可以很清楚的看到，抛出异常错误，解决方法就是：必须对其进行捕获或声明以便抛出，也就是我们必须要再加上一层 try...catch... 语句，如下：

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
			byte [] buffer = new byte[1024];
			while(true)
			{
				// 调用输入流对象的read方法，读取数据
				int temp = fis.read(buffer, 0, buffer.length);
				if(-1 == temp)
				{
					break;	// 如果读取完毕，就跳出
				}
				
				// 读出来多少数据，就写进去多少数据
				fos.write(buffer, 0, temp);				
				
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
				fis.close();
				fos.close();
			}
			catch(Exception e)
			{
				System.out.println(e);
			}			
		}
	}
}
```

&emsp;&emsp;此时运行结果如下，会发现没有任何输出，同样的，没有输出就是最好的结果

![image-20200530123228227](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200530123228.png)



# 2 字符流的使用方法

&emsp;&emsp;根据字面意思，就是在读写文件时，以字符为基础；

&emsp;&emsp;字符流的基本格式如下：

```java
// 字符输入流：Reader	FileReader
int read(char [] c, int off, int len)

// 字符输出流：Writer	FileWriter
int write(char [] c, int off, int len)
```

&emsp;&emsp;下面以实际代码为例，如下：

```java
import java.io.*;

public class TestChar
{
	public static void main(String args[])
	{
		FileReader fr = null;
		FileWriter fw = null;
		
		try
		{
			fr = new FileReader("from.txt");
			fw = new FileWriter("to.txt");
			
			// 字符流 生成char类型的
			char [] buffer = new char[100];	
			int temp = fr.read(buffer, 0, buffer.length);
			
			for(int i = 0; i < buffer.length; i++)
			{
				System.out.println(buffer[i]);
			}
		}
		catch(Exception e)
		{
			System.out.println(e);
		}
		finally
		{
			
		}
	}
}
```

&emsp;&emsp;上述代码，编译运行后的结果如下：

![image-20200530123746830](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200530123951.png)

&emsp;&emsp;会发现下边有好多空的，此时我们没有转换为字符串，而是直接打印数组中的结果，因此没有屏蔽结尾的换行等字符，因此就会出现这种结果。



# 3 总结

1. 对于比较大的文件的读写，先创建一个数组，数组小于文件大小，使用一个循环，然后用循环写入另外一个文件，什么时候停呢？条件为假的时候，什么时候为假？读完之后，read返回 -1 。
2. 简单了解了字节流、字符流的使用方法，特性等；
3. 还需继续努力呀！

> 如果文章内容有误，麻烦评论/私信多多指教，谢谢！如果觉得文章内容还不错，留个赞呗，您的点赞就是对我最大的鼓励，谢谢您嘞！