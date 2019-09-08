---
typora-copy-images-to: img
---

## 面向对象和面向过程

- 面向过程：因为面向对象中类调用实例化，开销大，消耗资源，性能差，而面向过程直接编译成机器码在电脑上执行。
- 面向对象：三大特性，低耦合使得系统更加灵活，容易维护。Java是半编译语言。

## 编译型和解释型

编译型：将源程序翻译成机器码，并存下来后续执行可以复用

解释型：源程序指令逐条解释执行。

java是半编译半解释型语言。

javac将源文件（.java)文件编译成字节码文件（.class文件），由jvm类加载器加载字节码文件，然后通过解释器逐行解释执行，速度慢；并且有些方法和代码块是经常需要被调用的(也就是所谓的热点代码)，所以后面引进了 JIT 编译器，而JIT 属于运行时编译。当 JIT 编译器完成第一次编译后，其会将字节码对应的机器码保存下来，下次可以直接使用。机器码的运行效率肯定是高于 Java 解释器的。

## JDK，JRE，JVM

**JDK:** Java Development Kit, Java开发工具箱,是给程序开发者用的。包括JRE，编译器（javac）和工具包。可以创建和编译程序。

**JRE:** 普通用户而只需要**安装JRE（Java Runtime Environment）来运行Java程序**。

**JVM：** 运行Java字节码的虚拟机，不同系统有不同的实现，“一次编译，到处运行”。

## Java和C++ 区别

- 都是面向对象的语言，都支持三大特性，封装、继承和多态
- Java不提供指针来直接访问内存，程序内存更加安全
- Java的类是单继承的，接口可以多继承。C++支持多重继承；
- Java有自动内存管理机制，不需要程序员手动释放无用内存

## Java和Python区别

语法方面：JAVA 里的块用大括号对包括，Python 以冒号 + 四个空格缩进表示。

类型声明：JAVA 的类型要声明，Python 的类型不需要。

分号：JAVA 每行语句以分号结束，Python 可以不写分号。

字符串：JAVA 中的字符串以**双引号**括起来，Python 中单引号或双引号

Python是强类型，动态类型，java是强类型，静态语言

强类型：不允许隐式类型转换。不允许不同类型相加。例如：整形+字符串会报类型错误。

弱类型：可以隐式类型转换。

静态类型：编译的时候就知道每一个变量的类型，因为类型错误而不能做的事情是语法错误。

动态类型：编译的时候不知道每一个变量的类型，因为类型错误而不能做的事情是运行时错误。譬如说你不能对一个数字a写a[10]当数组用。

## 三大特性

### 封装

将**不需要对外提供的内容**都隐藏起来。把属性都隐藏，提供**公共方法**对其访问。 java中通过将数据声明为私有的（private），对外提供公共的方法：getXxx()和setXxx()方法该属性其进行访问。

### 继承

1. 子类拥有父类对象所有的属性和方法（包括私有属性和私有方法），但是父类中的私有属性和方法子类是无法访问，**只是拥有**。
2. 子类可以拥有自己属性和方法，即子类可以对父类进行扩展。
3. 子类可以用自己的方式实现父类的方法。

<https://blog.csdn.net/a520songhai/article/details/80896633>

### 多态

父类型的引用指向子类型的对象。

多态的三个前提：要有**继承**关系，子类**重写**父类方法，父类引用指向子类对象

为什么用多态？

如果在实际的开发中发现某个类的方法可以做出某些改进，但由于工程已经交付给用户使用，就不想增加不必要的麻烦！但以后再次创建该类的对象时就需要改进过来。同时又不影响程序其他部分对该方法的调用。也就是说，如果再次创建该类的对象是不能做出改进的，应该由该类产生一个子类，并且子类将重写需要改进的方法，由于程序中其他地方需要调用该方法，所以对象的类型如果被创建成子类的类型的话将不能被有效调用，这就需要用到向上转换了即创建一个子类对象但是将其类型转换为父类的类型。这样做之后，程序的其他地方调用它时就能正确调用了，而且相应的方法也得到了改进。

原文链接：https://blog.csdn.net/kaweeee/article/details/77992336

向上转型，向下转型：通过引用类型判断。

成员函数：编译时看左边，运行时看右边。

## 数据类型

### 分类

基本数据类型分为三类：

1. 数值型：数值型又分为整数型和浮点型；
2. 字符型（char)
3. 布尔型（boolean)

为什么会有基本数据类型？

因为，在java中`new`一个对象是存储在堆里的，对于我们经常操作的数据类型，每次创建对象这样太消耗资源，因此java提供了8个基本数据类型，存储在栈里。用起来更方便。

### 8种基本数据类型

### 自动类型转换

转换前的数据类型的位数低于转换后的数据类型。

例如: short数据类型的位数为16位，就可以自动转换位数为32的int类型，同样float数据类型的位数为32，可以自动转换为64位的double类型。

```java
低  ------------------------------------>  高

byte—>short,char—> int —> long—> float —> double 
```

数据类型转换必须满足如下规则：

- 不能对boolean类型进行类型转换。

- 不能把对象类型转换成不相关类的对象。

- 由大到小会丢失精度：在把容量大的类型转换为容量小的类型时必须使用强制类型转换。

  强制类型转换

  - 条件是转换的数据类型必须是兼容的。
  - 格式：(type)value type是要强制类型转换后的数据类型

- 转换过程中可能导致溢出或损失精度，例如：

  ```
  int i =128;   
  byte b = (byte)i;//-128
  ```

  因为 byte 类型是 8 位，最大值为127，所以当 int 强制转换为 byte 类型时，值 128 时候就会导致溢出。

- 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入，例如：

  ```
  (int)23.7 == 23;        
  (int)-45.89f == -45
  ```

## 包装类

### 装箱

`Integer i = 100;`替代了 `Integer i = new Integer(100);`，因为Java帮我们提供了自动装箱的功能，不需要开发者手动去new一个Integer对象。

```java
Integer i = 100;//自动装箱
//相当于编译器自动作以下的语法编译：Integer i = Integer.valueOf(100);
```

### 拆箱

- 调用包装类中的.xxxValue()方法

  ```java
  Integer t = 128; // 此时t就是一个包装类
  System.out.println(t.intValue());//128
  ```

- 自动拆箱

  ```java
  Integer i = 10; //自动装箱 
  int t = i; //自动拆箱，实际上执行了 int t = i.intValue();
  ```

## 自动装箱和自动拆箱的实现原理

```java
Integer integer = 1;
//自动装箱，相当于Integer integer = Integer.valueOf(1);
int i = integer;
//自动拆箱,相当于int i = integer.intValue();
```

对于上面的代码，Java是怎么做的呢？

> 自动装箱：调用valueOf（）方法将原始类型值转换成对象
>
> 自动拆箱：调用intValue()方法，其他的（xxxValue())这类的方法将对象转换成原始类型值。

## 自动拆装箱与缓存

### 总结

- int 是基本数据类型
- Integer是包装类，`Integer i = num`，自动装箱而num值的范围如果取(-128<=num<=127)，那么就在`IntegerCache`中直接取已经创建好的对象，不会创建新的Integer对象
- `new Integer()` 在堆中创建新的Integer对象
- 无论是`Integer i1 = num`还是`Integer i2 = new Integer(num);`，i1与i2之间的比较`==`牵扯到对象的比较，对于对象比较,`==`比较的是地址。

具体请看下面的例子：

### Integer和int比较

> int 和 Integer在进行比较的时候，Integer会进行拆箱，转为int值与int进行比较

```java
@Test
public void testInteger(){
    Integer i = 10;
    int i1 = 10;
    System.out.println(i == i1); //true

    Integer i2 = 300;
    int i3 = 300;
    System.out.println(i2 == i3); //true
}
```

### Integer与Integer比较

Integer与Integer比较的时候，由于直接赋值的时候会进行自动装箱。那么这里就需要注意两个问题

1. -128<= x<=127的整数，将会直接缓存在IntegerCache中，那么当赋值在这个区间的时候，不会创建新的Integer对象，而是从缓存中获取已经创建好的Integer对象。
2. 大于这个范围的时候，直接new Integer来创建Integer对象。    

## 重写和重载

重载：

> 发生在同一个类中
>
> 记忆：同名不同参，返回值无关。
>
> 解释：参数列表不同：个数不同，数据类型不同，顺序不同。

重写：

> 子类对父类的方法的重写或者覆盖
>
> 同名同参同返回值

## 访问控制权限

> 简化记忆的方式（访问范围由小到大）:私下（private）里友好（friendly），才能更好地保护（protected）公众（public）。
>
> 具体说明：
>
> private使用范围仅限本类中 ；
>
> protected使用范围为含继承关系的类中（子类可以使用父类）； 
>
> 什么都不写叫友好类，默认是本包中；
>
> public特别随意，包内包外，类内类外都可访问 。
>
> **protected一个特点是只要子类都能访问，不管在不在一个包即可。**

![1565745112097](D:/JavaNote/Toffer/%E4%B8%B4%E6%97%B6%E5%9B%BE%E7%89%87%E6%96%87%E4%BB%B6%E5%A4%B9/1565745112097.png)

## final关键字

含义：声明类、 变量和方法时， 可使用关键字final来修饰,表示“ 最终的” 

> 特点
> final标记的类不能被继承。
>
> final标记的方法不能被子类重写。
>
> final标记的变量(成员变量或局部变量)即称为常量。 名称大写， 且只能被赋值一次。
> final double MY_PI = 3.14;
>
> final修饰引用保证引用不能指向别的对象，否则会报错。

## 代码块加载顺序

静态比非静态优先

1. 静态代码块和静态成员变量依据他们在代码中的前后顺序
2. 代码块和成员变量的顺序根据代码位置
3. 构造方法

如果有子父类继承的关系，顺序如下

1. 父类静态代码块或静态成员
2. 子类静态代码块或静态成员
3. 父类代码块或成员变量
4. 父类构造方法
5. 子类代码块或成员变量
6. 子类构造方法

```java
package com.ben;

/**
 * @ClassName: Demo
 * @author: benjamin
 * @version: 1.0
 * @description: TODO
 * @createTime: 2019/08/16/08:53
 */

public class Demo {
    public static void main(String[] args) {
        Cat cat = new Cat();
    }
}
class Animal{
    //静态代码块
    static {
        System.out.println("父类静态代码块");
    }
    // 静态变量
    static String name = "动物";
    // 构造器
    Animal(){
        System.out.println("父类构造器执行");
    }
    // 代码块
    {
        System.out.println("父类代码块执行");
    }
    // 静态方法
    static void eat(){
        System.out.println("父类静态方法+动物吃饭呢");
    }
    // 普通方法
    void play(){
        System.out.println("普通方法");
    }
}

class Cat extends Animal{
    //静态代码块
    static {
        System.out.println("子类静态代码块");
    }
    // 静态变量
    static String name = "动物";
    // 构造器
    Cat(){
        System.out.println("子类构造器执行");
    }
    // 代码块
    {
        System.out.println("子类代码块执行");
    }
    // 静态方法
    static void eat(){
        System.out.println("静态+猫吃饭呢");
    }
    // 普通方法
    void play(){
        System.out.println("普通方法");
    }
}
```

> 父类静态代码块
> 子类静态代码块
> 父类代码块执行
> 父类构造器执行
> 子类代码块执行
> 子类构造器执行

## this 和super的区别

super和this的区别

访问属性：

> this访问本类中的属性，本类无就去父类
>
> super访问父类属性

访问方法：

> this访问本类方法，本类无就去父类
>
> super访问父类方法

访问构造器

> this 调用本类构造器，放首行；
>
> super调用父类构造器，必须放在子类构造器的首行

## 抽象类与接口

1. 都不能直接被实例化，如果要实例化，需要有子类继承抽象类并实现抽象类中的所有方法，借助多态让接口定义的变量指向子类对象；
2. 抽象类需要被子类继承，接口需要被子类实现
3. 抽象类可以声明也可以实现，实现的时候就是普通方法，接口只能对方法声明
4. 抽象类中方法必须全部被子类实现，如果子类不能全部实现，子类还是抽象类；接口方法程序全部被子类实现，如果子类不能实现那么子类必须是抽象类
5. 抽象类中可以内有抽象方法
6. 抽象类中的方法都要被实现，所以抽象方法不能是static或private
7. 抽象类用来抽象类别，接口用来抽象方法功能。
8. 抽象类：像XXX一样 is a。接口：能XXX这样 like a

不同点：
（1）接口只有定义，不能有方法的实现，java 1.8中可以定义default方法体，而抽象类可以有定义与实现，方法可在抽象类中实现。

（2）一个类可以实现多个接口，但一个类只能继承一个抽象类。所以，使用接口可以间接地实现多重继承。
（3）接口成员变量默认为public static final，必须赋初值，不能被修改；其所有的成员方法都是public、abstract的。抽象类中成员变量默认default，可在子类中被重新定义，也可被重新赋值；抽象方法被abstract修饰，不能被private、static、synchronized和native等修饰，必须以分号结尾，不带花括号。

```java
public interface InterfaceDemo {

// 抽象方法
//    public abstract void method();// abstract可以省略，无方法体，供子类实现使用

// 含有默认方法和静态方法
public default void method(){};// default不能省，供子类调用或重写
public static void method2(){};// 供接口直接调用

// 含有私有方法和私有静态方法
//    private void method3(){} //jdk9加入，供接口中的默认方法或静态方法调用
}
```



Java中支持多继承吗：

支持，只不过java将多继承进行了改良，利用了多实现的方式，但是接口的出现实现了多继承，原因就在于接口的方法中没有方法体。

### 接口：

- 所有成员变量都默认是由public static final修饰的 
- 所有抽象方法都默认是由public abstract修饰的 
- 无构造器
- 多继承

![1567087331051](D:/JavaNote/Toffer/%E4%B8%B4%E6%97%B6%E5%9B%BE%E7%89%87%E6%96%87%E4%BB%B6%E5%A4%B9/1567087331051.png)

接口的实现：

- 先写extends，后写implements 
- 一个类可以实现多个接口，接口可以继承其他接口
- 实现接口的类必须把该接口中的所有方法都实现了，否则该类还是一个抽象类

jdk7.0之前，接口这种抽象类只包含常量和方法；

jdk8.0以后，接口可以添加静态方法和默认方法；

静态方法：static修饰；可以通过接口直接调用静态方法，执行方法体；

默认方法：default修饰；可以看到List源码中好多用default修饰的；

### 抽象类：

abstract修饰的一个类

abstract修饰的方法是抽象方法，只有声明，没有方法实现，分号结束。

含有抽象方法的类必须被声明为抽象类 

抽象类不能被实例化。抽象类是用来被继承的，抽象类的子类必须重写父类的抽象方法，并提供方法体。若没有重写全部的抽象方法，仍为抽象类。 

不能用abstract修饰变量、代码块、构造器 

不能用abstract修饰私有方法、静态方法、 final的方法、 final的类 



代码

```java
abstract class DemoA {
    int a = 666; // 常量

    abstract void haha(); //抽象方法

    void hehe() { // 普通方法

    }

    DemoA() {
        System.out.println("构造方法");
    }

    {
        System.out.println("代码块");
    }

    static {
        System.out.println("静态代码块");
    }
}

interface DemoB {
    int a = 11; // 默认修饰是public static final

    void start(); // 默认是public abstract

    public void run();

//    void stop(){ // 抽象方法不能有方法体
//
//    }

    // jdk8引入静态方法和默认方法
    static void hehe() {

    }

    default void haha() {

    }

    // private protected default public 
    public void play1();

    // protected void play2(); 报错，

    void play3();

    // private void play4(); 报错
    // 测试静态代码块,代码块，构造器都报错
//    static{
//        
//   }
//    {
//        
//    }
//    DemoB(){
//        
//    }
}
```

## 线程创建方式

一共四种：

继承Thead类

实现Runnable接口

实现Callable接口

线程池

## String

String和StringBuffer、StringBuilder的区别是什么？String为什么是不可变的？

可变与不可变：

> String类内部使用final修饰的字符数组保存字符串，`private　final　char　value[]`，所以String对象不可变的；
>
> StringBuffer和StringBuilder都继承于AbstractStringBuilder类，在该类内部使用字符数组保存字符串`char[] value`，无final修饰，所以可变。

线程安全性：

String 中的对象是不可变的，也就可以理解为常量，线程安全。

StringBuffer 类则每次都会对 StringBuffer 对象本身进行操作，而不是生成新的对象，再改变对象引用。所以在一般情况下我们推荐使用 StringBuffer ，特别是字符串对象经常改变的情况下

StringBuffer 对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。

StringBuilder 对方法没加同步锁，所以是非线程安全的。 

性能：

每次对 String 类型进行改变的时候，都会生成一个新的 String 对象，然后将指针指向新的 String 对象。StringBuffer 每次都会对 StringBuffer 对象本身进行操作，而不是生成新的对象并改变对象引用。相同情况下使用 StirngBuilder 相比使用 StringBuffer 仅能获得 10%~15% 左右的性能提升，但却要冒多线程不安全的风险。

1. 操作少量的数据 = String
2. 单线程操作字符串缓冲区下操作大量数据 = StringBuilder
3. 多线程操作字符串缓冲区下操作大量数据 = StringBuffer

总结：

> 不可变：String 是不可变的，底层使用final修饰的字符串数组存储，StringBuffer和StringBuilder继承于公共类AbstractStringBuilder，底层使用字符串数组存储，无final修饰。
>
> 底层源码：StringBuffer（）的扩容，默认初始容量为16，如果append一个字符串的长度大于16，先计算添加后的字符串大小，判断是否需要扩容，需要扩容的话就扩大为16*2+2 = 34，此时如果34还是小于字符串的长度，那么直接赋值该长度。再将扩容后的将原有数组中的元素复制到新的数组中。
>
> 线程安全：String对象不可变，线程安全；StringBuffer加锁，线程安全，StringBuilder未加锁，不安全
>
> 性能：
>
> 每次对String类型改变时，都会生成一个新的String对象，然后将指针指向新对象，适合少量数据
>
> StringBuffer对对象本身进行操作，线程安全。适合多线程，
>
> StringBuilder线程不安全，适合多线程。

## String的hashcode和toString

重写了Object类中的hashcode和toString方法

## 如果重写equals不重写hashcode会出现什么问题?

相等的对象必须具有相等的散列码





