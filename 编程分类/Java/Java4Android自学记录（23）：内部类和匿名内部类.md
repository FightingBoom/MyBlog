> 道阻且长，行则将至。埋头苦干，不鸣则已，一鸣惊人！加油，骚年！

# 目录及资源索引

&emsp;&emsp;[Java4Android自学过程目录及资源索引](https://blog.csdn.net/Fighting_Boom/article/details/103850497)

# 1 什么是内部类？

&emsp;&emsp;内部类：一个类定义在另一个类的里边，就把这种类称为内部类；代码举例如下：

```java
class A
{
    class B
    {
        
	}
}
```

&emsp;&emsp;此时如果直接编译，编译结果会是什么样呢？编译出来会有 2 个 class 文件，如下图：

![image-20200526224829631](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200526232753.png)

&emsp;&emsp;其中 A$B.class 就是内部类生成的类文件；

&emsp;&emsp;内部类编译后的名字，就是：==外部类名$内部类名.class==。



# 2 内部类有哪些语法特征？

## 2.1 如何生成内部类对象？

&emsp;&emsp;还是使用上述类文件，此时再重新创建一个类，用来存放 main 函数，程序内容如下：

```java
class Test
{
	public static void main(String args[]) 
	{
		A a = new A();				// 生成类A 对象
		
		A.B b = new A().new B();	// 生成子类B 对象
	}
}
```



## 2.2 内部类成员变量/函数的使用方法

&emsp;&emsp;我们先修改第一节的类文件，在其中添加部分成员变量，用以测试，具体代码如下：

```java
class A 
{
	int i;
	
	class B 
	{
		int j;
		
		int funB()
		{
			int result = i + j;
			System.out.println(result);		// 添加result打印，调试用
			return result;
		}
	}
}
```

&emsp;&emsp;此时再修改 main 函数，分别给类 A，类 B 中的成员变量赋值，查看函数输出结果

```java
class Test
{
	public static void main(String args[]) 
	{
		A a = new A();				// 生成类A 对象
		
		A.B b = a.new B();			// 生成子类B 对象
		
		a.i = 3;
		b.j = 1;
		b.funB();
	}
}
```

&emsp;&emsp;上述代码，编译运行后，结果如下：

![image-20200526230400661](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200526232753.png)

&emsp;&emsp;由代码及运行结果分析可得：

- 内部类可以随意使用外部类定义的成员变量。
- B 是 A 的内部类，意味着在B当中可以随意使用 A 当中的成员变量和成员函数，但是这不意味着 B 继承了 A，只是能使用而已，但是 B 并不拥有这些成员变量。
- 每一个内部类的对象都和一个外部类的对象相关联。也就是说有内部类对象，必然有一个跟他关联的外部类对象。
- 实际在内部类 B 中使用的变量 i ，就是外部类中的成员变量。



# 3 匿名内部类

&emsp;&emsp;匿名内部类：首先是内部类，其次没有名字，就叫匿名内部类；



&emsp;&emsp;下边用具体的代码进行实现，新建一个接口类 A

```java
interface A 
{
	public void doSomething();
}
```

&emsp;&emsp;接着定义一个类 B

```java
class B 
{
	public void fun(A a)
	{
		System.out.println("B类的fun函数");
		a.doSomething();
	}
}
```

&emsp;&emsp;此时类 B 需要一个 A 类型的对象，作为参数，还需要一个接口 A 的子类，因为 A 不能直接生成对象，具体如下：

```java
class AImpl implements A 
{
	public void doSomething()
	{
		System.out.println("doSomething");
	}
}
```

&emsp;&emsp;此时对主函数稍作修改，具体代码如下：

```java
class Test
{
	public static void main(String args[]) 
	{
		AImpl al = new AImpl();	// 生成子类对象
		A a = al;				// 向上转型
		
		B b = new B();
		b.fun(a);				// 传进去类型为A的参数
	}
}
```

&emsp;&emsp;上述代码编译运行结果如下：

![image-20200526232124996](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200526232125.png)



&emsp;&emsp;注意，如果此时使用匿名内部类，就会有一个不太正常的写法，修改主函数代码如下：

```java
class Test
{
	public static void main(String args[]) 
	{
		// AImpl al = new AImpl();	// 生成子类对象
		// A a = al;				// 向上转型
		
		B b = new B();
		b.fun(new A()
			{
				public void doSomething()
				{
					System.out.println("匿名内部类");
				}
			}
		);
	}
}
```

&emsp;&emsp;上述代码重新编译后，运行结果如下图：

![image-20200526232525713](https://raw.githubusercontent.com/FightingBoom/BlogPicture/master/20200526232730.png)

&emsp;&emsp;对匿名内部类代码及编译结果进行分析如下：

- 类B 的 fun 函数需要一个 A 类型的对象，和之前那个 AImpl 基本类似，但是没有名字；
- new A() 不能直接用，后边必须要跟上实现接口的类，但是没有名字，就叫匿名类；



# 4 总结

1. 了解内部类，内部类的基本语法特征，实现方式等；
2. 了解内部类成员变量、成员函数的使用方法，作用范围等；
3. 简单了解匿名内部类，特征及实现方式等。



> 如果文章内容有误，麻烦评论/私信多多指教，谢谢！如果觉得文章内容还不错，留个赞呗，您的点赞就是对我最大的鼓励，谢谢您嘞！