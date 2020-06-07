> 道阻且长，行则将至。埋头苦干，不鸣则已，一鸣惊人！加油，骚年！

# 前言
&emsp;&emsp;根据《C++ Primer》，第二章《变量和基本类型》总结而来；

&emsp;&emsp;提示：善于利用 Ctrl + F 快捷键，快速搜索相关内容哦！

# 1 本章小结
1. 类型是 C++ 编程的基础；
2. 类型规定了其对象的存储要求和所能执行的操作；
3. 类型分为非常量和常量，常量对象必须初始化，而且一旦初始化其值就不能再改变；
4. 此外，还可以定义复合类型，如指针和引用等；复合类型的定义以其他类型为基础；
5. <font color=#ff0000 size=3>C++ 语言允许用户以类的形式自定义类型。C++ 库通过类提供了一套高级抽象类型，如输入输出和 string 等。</font>

# 2 术语表正文
 - <font color=#ff0000 size=3> `地址（address）` </font>：是一个数字，根据它可以找到内存中的一个字节。

 - <font color=#ff0000 size=3> `别名声明（alias declaration）` </font>：为另外一种类型定义一个同义词：使用 “名字 = 类型” 的格式将名字作为该类型的同义词。

 - <font color=#ff0000 size=3> `算数类型（arithmetic type）` </font>：布尔值、字符、整数、浮点数等内置类型。

 - <font color=#ff0000 size=3> `数组（array）` </font>：是一种数据结构，存放着一组未命名的对象，可以通过索引来访问这些对象。

 - <font color=#ff0000 size=3> `auto` </font>：是一个类型说明符，通过变量的初始值来推断变量的类型。

 - <font color=#ff0000 size=3> `基本类型（base type）` </font>：是类型说明符，可以用 const 修饰，在声明语句中位于声明符之前。基本类型提供了最常见的数据类型，以此为基础构建声明符。

 - <font color=#ff0000 size=3> `绑定（bind）` </font>：令某个名字与给定的实体关联在一起，使用该名字也就是使用该实体。例如，引用就是将某个名字与某个对象绑定在一起。

 - <font color=#ff0000 size=3> `字节（byte）` </font>：内存中可寻址的最小单元，大多数机器的字节占8位。

 - <font color=#ff0000 size=3> `类成员（class member）` </font>：类的组成部分。

 - <font color=#ff0000 size=3> `复合类型（compound type）` </font>：是一种类型，它的定义以其他类型为基础。

 - <font color=#ff0000 size=3> `const` </font>：是一种类型修饰符，用于说明永不改变的对象。const 对象一旦定义就无法再赋新值，所以必须初始化。

 - <font color=#ff0000 size=3> `常量指针（const pointer）` </font>：是一种指针，它的值永不改变。

 - <font color=#ff0000 size=3> `常量引用（const reference）` </font>：是一种习惯叫法，含义是指向常量的引用。

 - <font color=#ff0000 size=3> `常量表达式（const expression）` </font>：能在编译时计算并获取结果的表达式。

 - <font color=#ff0000 size=3> `constexpr` </font>：是一种函数，用于代表一条常量表达式。

 - <font color=#ff0000 size=3> `转换（conversion）` </font>：一种类型的值转变成另外一种类型值的过程。C++ 语言支持内置类型之间的转换。

 - <font color=#ff0000 size=3> `数据成员（data member）` </font>：组成对象的数据元素，类的每个对象都有类的数据成员的一份拷贝。数据成员可以在类内部声明的同时初始化。

 - <font color=#ff0000 size=3> `声明（declaration）` </font>：声称存在一个变量、函数或是别处定义的类型。名字必须在定义或声明之后才能使用。

 - <font color=#ff0000 size=3> `声明符（declarator）` </font>：是声明的一部分，包括被定义的名字和类型修饰符，其中类型修饰符可以有也可以没有。

 - <font color=#ff0000 size=3> `decltype` </font>：是一个类型说明符，从变量或表达式推断得到类型。

 - <font color=#ff0000 size=3> `默认初始化（default initialization）` </font>：当对象未被显式地赋予初始值时执行的初始化行为。由类本身负责执行的类对象的初始化行为。全局作用域的内置类型对象初始化为 0；局部作用域的对象未被初始化即拥有未定义的值。

 - <font color=#ff0000 size=3> `定义（definition）` </font>：为某一特定类型的变量申请存储空间，可以选择初始化该变量。名字必须在定义或声明之后才能使用。

 - <font color=#ff0000 size=3> `转义序列（escape sequence）` </font>：字符特别是那些不可打印字符的替代形式。转义以反斜线开头，后面紧跟一个字符，或者不多于 3 个八进制数字，或者字母 x 加上 1 个十六进制数。

 - <font color=#ff0000 size=3> `全局作用域（global scope）` </font>：位于其他所有作用域之外的作用域。

 - <font color=#ff0000 size=3> `头文件保护符（header guard）` </font>：使用预处理变量以防止头文件被某个文件重复包含。

 - <font color=#ff0000 size=3> `标识符（identifier）` </font>：组成名字的字符序列，标识符对大小写敏感。

 - <font color=#ff0000 size=3> `类内初始值（in-class initializer）` </font>：在声明类的数据成员时同时提供的初始值，必须置于等号右侧或花括号内。

 - <font color=#ff0000 size=3> `在作用域内（in scope）` </font>：名字在当前作用域内可见。

 - <font color=#ff0000 size=3> `被初始化（initialized）` </font>：变量在定义的同时被赋予初始值，变量一般都应该被初始化。

 - <font color=#ff0000 size=3> `内层作用域（inner scope）` </font>：嵌套在其他作用域之内的作用域。

 - <font color=#ff0000 size=3> `整形（integral type）` </font>：参见算术类型。

 - <font color=#ff0000 size=3> `列表初始化（list initialization）` </font>：利用花括号把一个或多个初始值放在一起的初始化形式。

 - <font color=#ff0000 size=3> `字面值（literal）` </font>：是一个不能改变的值，如数字、字符、字符串等。单引号内的是字符字面值，双引号内的是字符串字面值。

 - <font color=#ff0000 size=3> `局部作用域（local scope）` </font>：是块作用域的习惯叫法。

 - <font color=#ff0000 size=3> `底层 const （low-level const）` </font>：一个不属于顶层的 const ，类型如果由底层常量定义，则不能被忽略。

 - <font color=#ff0000 size=3> `成员（member）` </font>：类的组成部分。

 - <font color=#ff0000 size=3> `不可打印字符（nonprintable character）` </font>：不具有可见形式的字符，如控制符、退格、换行符等。

 - <font color=#ff0000 size=3> `空指针（null pointer）` </font>：值为 0 的指针，空指针合法但是不指向任何对象。

 - <font color=#ff0000 size=3> `nullptr` </font>：是表示空指针的字面值常量。

 - <font color=#ff0000 size=3> `对象（object）` </font>：是内存的一块区域，具有某种类型，变量是命名了的对象。

 - <font color=#ff0000 size=3> `外层作用域（outer scope）` </font>：嵌套着别的作用域的作用域。

 - <font color=#ff0000 size=3> `指针（pointer）` </font>：是一个对象，存放着某一个对象的地址，或者某个对象存储区域之后的下一地址，或者 0 。

 - <font color=#ff0000 size=3> `指向常量的指针（pointer to const）` </font>：是一个指针，存放着某个常量对象的地址。指向常量的指针不能用来改变它所指对象的值。

 - <font color=#ff0000 size=3> `预处理器（preprocessor）` </font>：在 C++ 编译过程中执行的一段程序。

 - <font color=#ff0000 size=3> `预处理变量（preprocessor variable）` </font>：由预处理器管理的变量。在程序编译之前，预处理器负责将程序中的预处理变量替换成它的真实值。

 - <font color=#ff0000 size=3> `引用（reference）` </font>：是某个对象的别名。

 - <font color=#ff0000 size=3> `对常量的引用（reference to const）` </font>：是一个引用，不能用来改变它所绑定对象的值。对常量的引用可以绑定常量对象，或者非常量对象，或者表达式的结果。

 - <font color=#ff0000 size=3> `作用域（scope）` </font>：是程序的一部分，在其中某些名字有意义。C++ 有几级作用域：
	- <font color=#ff0000 size=3> `全局（global）` </font>：名字定义在所有其他作用域之外。
	- <font color=#ff0000 size=3> `类（class）` </font>：名字定义在类内部。
	- <font color=#ff0000 size=3> `命名空间（namespace）` </font>：名字定义在命名空间内部。
	- <font color=#ff0000 size=3> `块（block）` </font>：名字定义在块内部。

&emsp;&emsp;名字从声明位置开始直至声明语句所在的作用域末端为止都是可用的。

 - <font color=#ff0000 size=3> `分离式编译（separate compilation）` </font>：把程序分割为多个单独文件的能力。

 - <font color=#ff0000 size=3> `带符号类型（signed）` </font>：保存正数、负数或 0 的整型。

 - <font color=#ff0000 size=3> `字符串（string）` </font>：是一种库类型，表示可变长字符序列。

 - <font color=#ff0000 size=3> `struct` </font>：是一个关键字，用于定义类。

 - <font color=#ff0000 size=3> `临时值（temporary）` </font>：编译器在计算表达式结果时创建的无名对象。为某表达式创建了一个临时值，则此临时值将一直存在直到包含有该表达式的最大的表达式计算完成为止。

 - <font color=#ff0000 size=3> `顶层 const （top-level const）` </font>：是一个 const ，规定某对象的值不能改变。

 - <font color=#ff0000 size=3> `类型别名（type alias）` </font>：是一个名字，是另外一个类型的同义词，通过关键字 typedef 或别名声明语句来定义。

 - <font color=#ff0000 size=3> `类型检查（type checking）` </font>：是一个过程，编译器检查程序使用某给定类型对象的方式与该类型的定义是否一致。

 - <font color=#ff0000 size=3> `类型说明符（type specifier）` </font>：类型的名字。

 - <font color=#ff0000 size=3> `typedef ` </font>：为某类型定义一个别名。当关键字 typedef 作为声明的基本类型出现时，声明中定义的名字就是类型名。

 - <font color=#ff0000 size=3> `未定义（undefined）` </font>：即 C++ 语言没有明确规定的情况。不论是否有意为之，未定义行为都可能引发难以追踪的运行时错误、安全问题和可移植性问题。（举例：vector向量使用 v[]，如果下标越界，则函数行为未定义；但是使用 v.at()，虽然也有错误，但是会抛出异常）

 - <font color=#ff0000 size=3> `未初始化（uninitialized）` </font>：变量已定义但未被赋予初始值。一般来说，试图访问未初始化变量的值将引发未定义行为。

 - <font color=#ff0000 size=3> `无符号类型（unsigned）` </font>：保存大于等于 0 的整型。

 - <font color=#ff0000 size=3> `变量（variable）` </font>：命名的对象或引用。C++ 语言要求变量要先声明后使用。

 - <font color=#ff0000 size=3> `void*` </font>：可以指向任意非常量的指针类型，不能执行解引用操作。

 - <font color=#ff0000 size=3> `void 类型` </font>：是一种有特殊用处的类型，既无操作也无值。不能定义一个 void 类型的变量。

 - <font color=#ff0000 size=3> `字（Word）` </font>：在指定机器上进行整数运算的自然单位。一般来说，字的空间足够存放地址。32 位机器上的字通常占据 4 个字节。

 - <font color=#ff0000 size=3> `& 运算符（& operator）` </font>：取地址运算符。

 - <font color=#ff0000 size=3> `* 运算符（* operator）` </font>：解引用运算符。解引用一个指针将返回该指针所指的对象，为解引用的结果复制也就是为指针所指的对象赋值。

 - <font color=#ff0000 size=3> `#define` </font>：是一条预处理指令，用于定义一个预处理变量。

 - <font color=#ff0000 size=3> `#endif` </font>：是一条预处理指令，用于结束一个 #ifdef 或 #ifndef 区域。

 - <font color=#ff0000 size=3> `#ifdef` </font>：是一条预处理指令，用于判断给定的变量是否已经定义。

 - <font color=#ff0000 size=3> `#ifndef ` </font>：是一条预处理指令，用于判断给定的变量是否尚未定义。

> 如果文章内容有误，麻烦评论/私信多多指教，谢谢！如果觉得文章内容还不错，留个赞呗，您的点赞就是对我最大的鼓励，谢谢您嘞！