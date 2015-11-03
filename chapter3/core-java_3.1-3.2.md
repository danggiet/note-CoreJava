//core-java reading notes  
//按阅读顺序，读到什么写什么   准备按书上章节标题  
//节节3行，段落分2行，段内1行 标题空一行 单线  节节双线
＃第三章    java的基本程序设计结构

-   [用一个简单的java程序开始](#一个简单的java程序)
-   [注释](#注释)
-   [java的数据类型](#数据类型)
-   [变量](#变量)
-   [运算符](#运算符)
-   [字符串](#字符串)
-   [I/O](#I/O)
-   [控制结构](#控制结构)
-   [大数值](#大数值)
-   [数组](#数组)

---
本章主要介绍java程序设计相关的基本概念（数据类型，分支，循环）

---
<a name="一个简单的java程序"></a> 
##从一个简单的程序开始
//主要讲了类和方法
    ```java
        //first simple java sample  
    public Class FistSample
    {  
        public static void main (string[] args)
            {  
                System.out.println("we'll not use 'hello,world!'");  
            }       
        }   
    ```  
* public:   access modifer  用于控制程序的其他部分对这段代码的访问级别.第5章讲。  
)

* Class:    类。类是构建所有java应用程序和appplet的构建块。  
源代码的文件名必须与公共类的类名相同。并用.java做扩展名  
因此储存这段代码的文件名必须为 FirstSample.java ,编译这个源文件后将得到这个类的字节码文件FirstSample.class
>类名的标准命名规范：  
>>类名必须以大写字母开头， 
>>如果由多个单词组成，每个单词的首字母要大写（驼峰命名法）


当使用 java ClassName运行编译程序时，java虚拟机将从指定类中的main函数开始执行。因此为了代码能够执行，在类的源文件中必须有main函数。当然，用户在类中自定义函数，并在main中调用他们。

java规定main方法必须声明为public，

##由类名的命名规范总结到java的命名规范
{

}

---
运行、编译程序时，java虚拟机将从指定类中的main方法开始执行。因此为了代码能够执行，必须在  
源文件中包含一个main方法。（有多个main方法可以吗？）  
用户自己定义的函数添加到类中，在main中调用它们。  


 java规定main方法必须声明为public 

 java与c++中类的差异：
    >java的所有内容都放在类中，因此java中的main方法必须有一个外壳类。 
    >java规定main方法必须是静态的。(为什么？)

再来看这段代码：
    ```java
    {
        System.out.println("we'll not use 'hello world'");  
    }
    ```
    >使用了System.out对象，并调用了println方法  
    >点号（.)用于调用方法  
    >通用语法：object.method(parameters)
    >上面的System.out 是object ,parameter 是 字符串  
    >java与c、c++ 一样，使用双引号分隔字符串  
    >在java的方法中，即使没有参数也要使用括号。`println()打印一个空行`  
    >System.out还有一个 print 方法，打印后不换行。 



---
<a name="注释"></a>
##注释

java有三种注释方式  
// 单行注释  
/*...*/     多行注释  
/**...*/    可以自动生成文档。第四章讲
这里，不管是java还是c，/*..*/注释不能嵌套。


---
<a name="数据类型"></a>
##java中的数据
java是一种强类型语言：意思是必须为每一个变量声明其类型。java一共有8种基本类型（primitive   type).4种整型（int.short.long.byte)、2种浮点型、表示Unicode字符编码的 char   类型，表示真值的boolean类型。

java中每一种类型的数据取值范围是固定的（java中所有的数据类型所占据的字节数量是固定的），不像c语言每种数据占用的字节依赖于具体的cpu。

java没有无符号类型(unsigned)

### 整型
按大小排列：
byte    1字节 －128～127        (2^7=128)   
short   2字节 －32768～32767    (2^15=2^10*2^5=1024*32=32768)
int     4字节 -2,147,483,648~2,147,483,647（20亿）
｀经计算得2^31，推出一个字节8位。一个位用来存符号。
long    8字节 －2^63~2^63-1

可以看出，超过20亿，就需要使用long类型了。因此描述地球上的人数就得使用long型整数。

关于进制的前缀：8进制数值有一个前缀0，16进制前缀0X,2进制前缀0b


###浮点型
浮点类型用于表示有小数部分的数值。java中有两种浮点类型：
float   4字节 取值范围没看懂
double  8字节 应该可以参考c书上的浮点值的表示方法

java小数中默认为 double 类型，因此要注明一个数是float需要在后面加后缀F(3.14F)
        ```0x1.0p-3
        16进制中，用p表指数（不是e），
        尾数采用16进制，
        指数采用10进制（   貌似其它进制的数指数也都是采用10进制）
        指数的基数是2，不是10
        {1*16^0+0*16^(-1)}*2^(-3)=1/8=0.125
        ```

所有的浮点数计算都遵循 IEEE 754 规范。什么东东？

<a name="3个特殊的浮点值"></a>
用来表示溢出和出错情况的3个**特殊**浮点值:
*   正无穷 一个正整数除以0（正数可以么？）在后面可以看到是不可以的。
*   负无穷 
*   NaN(Not a Number)  0/0 或者 负数的平方根 
```
    常量  Double.POSITIVE_INFINITY Double.NEGATIVE_INFINITY 和 Double.NaN
    分别表示这三个特殊的值。

    关于Double.NaN:不能这样检测一个特定的值是否等于 Double.NaN
    if(x==Double.NaN)   //is NEVER ture !
    因为所有“非数值”的值都认为是不相同的。
    可以使用 Double.isNaN 方法：
    if（Double.isNaN(x))     //check whether x is 'not a number' 
```




---
###char类型
char用来表示单个字符常量，'A'是编码65对应的字符常量，“A"是一个包含字符A的字符串。
Unicode编码单元若用16进制表示，其范围从\u0000到\uffff。
    ```16*16^3+16*16^2+16*16+16=   
        65536 + 4096 + 256 + 16= 69904
        发现是不能被1024整除的。
        ASCII只需要8位，128位字符。
    ```

###转义序列符：
* 转义序列符/u表示Unicode编码,\u03C0表示希腊字母PI
* 还有一些表示特殊字符的转义字符。
* 表示特殊字符的转义序列必须放在引号内，唯独/u还可以出现在引号外。

>为什么要设定Unicode编码表？：
* 1991年发布Unicode 1.0,采用16位编码，当时仅占用65536个代码值中不到一半的部分，
* 经过一段时间，随着字符的扩增，字符数超过了65536，16位的char类型已经不能满足需要了，

那么java是如何解决这个问题的呢？
先来介绍一些专业术语：
1. 代码点（code point): 编码表中与某个字符相对应的*代码值*。
    >代码点才用16进制编写，并在前面加上前缀`u+`,例如u+0041就是字母A的代码点。
    >代码点可以分为17个代码级别:
    * 第一个级别称为基本的多语言级别（basical multilingual plane),代码点从U+0000到U+FFFF
    * 其余的16个代码级别从U+10000到U+10FFFF,包括一些辅助字符。
2. 更详细的再去wiki搜索utf－16。

UTF-16编码采用不同长度的编码表示所有Unicode代码点。
    >* 在基本的多语言级别中，每个字符用16位表示，被称为代码单元(code unit)。
    >* 辅助字符采用一对连续的代码单元表示。



---
<a name="boolean类型"></a>
###boolean类型
boolean有两个值， false和true。
整型值和布尔值之间不能相互转换。而在c中，0相当于布尔值false，非0相当于true。
    ```
    if(x=0)  //oops...meant x==0 
     在c／c++中可以运行，因为表达式的值0可以转换成布尔值0；
     在java中则不能通过编译，因为java中整数不能转换成布尔值；
     ```




---     
---
<a name="变量">
###变量
变量名由字母数字$, 下划线组成。但必须由字母开头。
* 声明变量：在变量名前加类型名声明变量。

---
####变量的声明和初始化
声明一个变量之后，必须用赋值语句对变量进行__显式__初始化。变量使用前必须初始化。
声明和初始化可以放在同一行中：`int vacationDays=12;`
java中可以在代码中任何地方声明变量。如：
    ```java
    double salary=65000.0;
    System.out.printl(salary);
    int vacationDays=12;        //Ok to declare a variable here
    ```
在java中，变量的声明尽可能放在变量第一次使用的地方，这是一种良好的编程习惯。


    在c／c++中区分变量的___声明___和___定义___
    int i=0;  // 这是一个定义
    extern int i; //这是一个声明。
    ___在java中不区分变量的声明和定义。

####常量
用关键字final定义常量。 final：固定的，不可变的。
习惯上，常量名使用全大写。
    ```java
    final double CM_PER_INCH=2.54；
    ```

*   类常量：
    * 该常量能被该类中所有的方法使用。
    * 使用关键字`static final`设置类常量。
    ```java
    public class Constants2
    {
        public static final double CM_PER_INCH=2.54;//这里类定义为public，其它类的函数也可以调用这个常数。
        public void main(String[] args)
        {
            double paperWidth=8.5;
            double paperHight=11;
            System.out.println("paper size in centimeters:"+paperWidth*CM_PER_INCH+"by"+paperHight*CM_PER_INCH);
        }
    }
    ```

类常量要在 ___main___ 方法外部定义。
同一类中的其它方法可以使用这个常量，如果该类常量被声明为public,那么其他类的方法也可以使用这个常量！
* const是java保留的关键字，做什么用的现在还不知道。但是知道java中声明常量必须用final。



---
<a name="运算符"></a>
###运算符
*   当参与／的两个操作数都是整数时，表示整数除法；否则，表示浮点除法。两个新认识：
         *  取整：取商的整数部分
         *  要求商的全部数值时，采用浮点除法（15.0/2=7.5）
*   当除数为0时：
    1.  整数被0除会发生异常。
    2.  浮点数被0除会得到___无穷大___ 或___NaN___ 结果
        因为前面说了，无穷大和NaN这三个常量属于double类型的。[3个特殊的浮点值](#3个特殊的浮点值)

*   strictfp严格浮点运算：

>double类型使用64位储存一个double值，而有些cpu使用80位浮点寄存器。
这些寄存器增加了中间过程的计算精度：
double w=x*y/z;
很多intel处理器计算x*y,并将结果寄存在80位的寄存器中，再除以z并将；结果截尾成64位。这样的到的结果比较精确。
还能避免产生指数溢出？
但是这个结果可能与64位机器上的计算结果不一样。
对于使用strictfp标记的方法 `public static strict void main(String[] args){...}`,main方法中的所有指令都要采用严格的浮点计算。
具体以后再翻阅wiki java中间计算 指数溢出..


        






























