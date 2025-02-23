# Java基础（from 尚硅谷 - 宋红康）

# 

# 1、基本数据类型

## 1.1 整数类型

- Java各整数类型有固定的表数范围和字段长度，不受具体操作系统的影响，以保证Java程序的可移植性。

<img src="http://jason243.online/javase_songhongkang/002/images/image-20220311001553945.png" alt="image-20220311001553945" style="zoom:80%;" />

- 定义long类型的变量，赋值时需要以"`l`"或"`L`"作为后缀。
- Java程序中变量通常声明为int型，除非不足以表示较大的数，才使用long。
- Java的整型`常量默认为 int 型`。

## 1.2 浮点类型：float、double

- 与整数类型类似，Java 浮点类型也有固定的表数范围和字段长度，不受具体操作系统的影响。

<img src="http://jason243.online/javase_songhongkang/002/images/image-20220311001749699.png" alt="image-20220311001749699" style="zoom:80%;" />

- 浮点型常量有两种表示形式：
  - 十进制数形式。如：5.12       512.0f        .512   (必须有小数点）
  - 科学计数法形式。如：5.12e2      512E2     100E-2
- float：`单精度`，尾数可以精确到7位有效数字。很多情况下，精度很难满足需求。    
- double：`双精度`，精度是float的两倍。通常采用此类型。
- 定义float类型的变量，赋值时需要以"`f`"或"`F`"作为后缀。
- Java 的浮点型`常量默认为double型`。

### 1.2.1 关于浮点型精度的说明

- 并不是所有的小数都能可以精确的用二进制浮点数表示。二进制浮点数不能精确的表示0.1、0.01、0.001这样10的负次幂。
- 浮点类型float、double的数据不适合在`不容许舍入误差`的金融计算领域。如果需要`精确`数字计算或保留指定位数的精度，需要使用`BigDecimal类`。

## 1.3 字符类型：char

- char 型数据用来表示通常意义上“`字符`”（占2字节，底层使用`UTF-16`编码）

- Java中的所有字符都使用Unicode编码，故一个字符可以存储一个字母，一个汉字，或其他书面语的一个字符。

- 字符型变量的三种表现形式：

  - **形式1：**使用单引号(' ')括起来的`单个字符`。

    例如：char c1 = 'a';   char c2 = '中'; char c3 =  '9';

  - **形式2：**直接使用 `Unicode值`来表示字符型常量：‘`\uXXXX`’。其中，XXXX代表一个十六进制整数。

    例如：\u0023 表示 '#'。

  - **形式3：**Java中还允许使用`转义字符‘\’`来将其后的字符转变为特殊字符型常量。

    例如：char c3 = '\n';  // '\n'表示换行符

  | 转义字符 |  说明  | Unicode表示方式 |
  | :------: | :----: | :-------------: |
  |   `\n`   | 换行符 |     \u000a      |
  |   `\t`   | 制表符 |     \u0009      |
  |   `\"`   | 双引号 |     \u0022      |
  |   `\'`   | 单引号 |     \u0027      |
  |   `\\`   | 反斜线 |     \u005c      |
  |   `\b`   | 退格符 |     \u0008      |
  |   `\r`   | 回车符 |     \u000d      |

- char类型是可以进行运算的。因为它都对应有Unicode码，可以看做是一个数值。

## 1.4 布尔类型：boolean

- boolean 类型用来判断逻辑条件，一般用于流程控制语句中：
  - if条件控制语句；                  
  - while循环控制语句；     
  - for循环控制语句；
  - do-while循环控制语句； 
- **boolean类型数据只有两个值：true、false，无其它。**
  - **不可以使用0或非 0 的整数替代false和true，这点和C语言不同。**
  - 拓展：Java虚拟机中没有任何供boolean值专用的字节码指令，Java语言表达所操作的boolean值，在编译之后都使用java虚拟机中的int数据类型来代替：true用1表示，false用0表示。——《java虚拟机规范 8版》

> 经验之谈：
>
> Less is More！建议不要这样写：if ( isFlag = = true )，只有新手才如此。关键也很容易写错成if(isFlag = true)，这样就变成赋值isFlag为true而不是判断！`老鸟的写法`是if (isFlag)或者if ( !isFlag)。







# ======

# 2、引用数据类型

## 2.1 String

### 2.1.1 字符串类型：String

- String不是基本数据类型，属于引用数据类型
- 使用一对`""`来表示一个字符串，内部可以包含0个、1个或多个字符。
- 声明方式与基本数据类型类似。例如：String str = “尚硅谷”;

### 2.1.2 运算规则

**1、任意八种基本数据类型的数据与String类型只能进行连接“+”运算，且结果一定也是String类型**

```java
System.out.println("" + 1 + 2);//12

int num = 10;
boolean b1 = true;
String s1 = "abc";

String s2 = s1 + num + b1;
System.out.println(s2);//abc10true

//String s3 = num + b1 + s1;//编译不通过，因为int类型不能与boolean运算
String s4 = num + (b1 + s1);//编译通过
```

**2、String类型不能通过强制类型()转换，转为其他的类型**

```java
String str = "123";
int num = (int)str;//错误的

int num = Integer.parseInt(str);//正确的，后面才能讲到，借助包装类的方法才能转
```



## 2.2 数组

### 2.2.1 一维数组

#### 2.2.1.1 一维数组的声明

**格式：**

```java
//推荐
元素的数据类型[] 一维数组的名称;

//不推荐
元素的数据类型  一维数组名[];
```

**举例：**

```java
int[] arr;
int arr1[];
double[] arr2;
String[] arr3;  //引用类型变量数组
```

**数组的声明，需要明确：**

（1）数组的维度：在Java中数组的符号是[]，[]表示一维，\[]\[]表示二维。

（2）数组的元素类型：即创建的数组容器可以存储什么数据类型的数据。元素的类型可以是任意的Java的数据类型。例如：int、String、Student等。

（3）数组名：就是代表某个数组的标识符，数组名其实也是变量名，按照变量的命名规范来命名。数组名是个引用数据类型的变量，因为它代表一组数据。

注意：Java语言中声明数组时不能指定其长度(数组中元素的个数)。 例如： int a[5]; //非法

#### 2.2.1.2 一维数组的初始化

##### 2.2.1.2.1 静态初始化

- **如果数组变量的初始化和数组元素的赋值操作同时进行，那就称为静态初始化。**
- **一维数组声明和静态初始化格式1：**

```java
int[] arr = new int[]{1,2,3,4,5};//正确
//或
int[] arr;
arr = new int[]{1,2,3,4,5};//正确
```

- **一维数组声明和静态初始化格式2**：

```java
int[] arr = {1,2,3,4,5};//正确

int[] arr;
arr = {1,2,3,4,5};//错误
```

##### 2.2.1.2.2 动态初始化

**数组变量的初始化和数组元素的赋值操作分开进行，即为动态初始化。**

- [长度]：数组的长度，表示数组容器中可以最多存储多少个元素。
- **注意：数组有定长特性，长度一旦指定，不可更改。**和水杯道理相同，买了一个2升的水杯，总容量就是2升是固定的。

**举例1：正确写法**

```java
int[] arr = new int[5];

int[] arr;
arr = new int[5];
```

### 2.2.2  数组的长度

- **每个数组都有一个属性length指明它的长度，例如：arr.length 指明数组arr的长度(即元素个数)**
- 每个数组都具有长度，而且一旦初始化，其长度就是确定，且是不可变的。

### 2.2.3 数组元素的默认值

数组是引用类型，当我们使用动态初始化方式创建数组时，元素值只是默认值。

对于基本数据类型而言，默认初始化值各有不同。

对于引用数据类型而言，默认初始化值为null（注意与0不同！)

![数组元素默认值表](http://jason243.online/javase_songhongkang/005/images/1561509460135.png)

### 2.2.4 两个变量指向一个一维数组

两个数组变量本质上代表同一个数组。

```java
public static void main(String[] args) {
    // 定义数组，存储3个元素
    int[] arr = new int[3];
    //数组索引进行赋值
    arr[0] = 5;
    arr[1] = 6;
    arr[2] = 7;
    
    int[] arr2 = arr; // 赋值的是引用，浅拷贝
    arr2[1] = 9;
    System.out.println(arr[1]);
}
```



### 2.2.5 Arrays 工具类的详细介绍与使用示例

#### 2.2.5.1. **数组元素拼接 Arrays.toString**

- **`static String toString(int[] a)`** 
  拼接整型数组
- **`static String toString(Object[] a)`** 
  拼接对象数组。如果对象未重写 `toString()`，返回类型和哈希值。

#### 2.2.5.2. **数组排序 Arrays.sort**

- **`static void sort(int[] a)`** 
  对整型数组进行升序排序。
- **`static void sort(int[] a, int fromIndex, int toIndex)`** 
  对部分数组（区间 `[fromIndex, toIndex)`）进行升序排序。
- **`static void sort(Object[] a)`** 
  对对象数组进行升序排序，要求对象实现了 `Comparable` 接口。
- **`static <T> void sort(T[] a, Comparator<? super T> c)`** 
  使用自定义比较器对对象数组排序。

#### 2.2.5.3. **数组元素的二分查找 Arrays.binarySearch**

- **`static int binarySearch(int[] a, int key)`** 
  在整型数组中查找 `key` 的位置。
- **`static int binarySearch(Object[] a, Object key)`** 
  在对象数组中查找 `key` 的位置，数组必须是有序的。

> **排序算法说明**
>
> 1. **基本数据类型（如 int[], double[] 等）**
>
> 对于基本数据类型的排序，`Arrays.sort()` 使用了 **双轴快速排序（Dual-Pivot QuickSort）**，该算法由 Vladimir Yaroslavskiy 开发，并在 Java 7 中引入。
>
> 2. **引用数据类型（如 String[], Object[] 等）**
>
> 对于引用数据类型的排序，`Arrays.sort()` 使用了 **归并排序（TimSort）**。
>

#### 2.2.5.4. **数组的复制 Arrays.copyOf**

- **`static int[] copyOf(int[] original, int newLength)`** 
  创建一个新的整型数组，长度为 `newLength`。
  
- **`static <T> T[] copyOf(T[] original, int newLength)`** 
  创建一个新的泛型数组。
  
- **`static int[] copyOfRange(int[] original, int from, int to)`** 
  创建一个新的整型数组，内容为原数组的 `[from, to)` 部分。
  
- **`static <T> T[] copyOfRange(T[] original, int from, int to)`** 
  创建一个新的泛型数组。
  
  > `Arrays.copyOf` 的调用的是 `System.arraycopy` 方法
  >
  > `System.arraycopy` 是 Native方法
  >
  > ```java
  > System.arraycopy(original, 0, copy, 0, Math.min(original.length, newLength));
  > ```

#### 2.2.5.5. **比较两个数组是否相等 Arrays.equals**

- **`static boolean equals(int[] a, int[] a2)`** 
  比较两个整型数组。
- **`static boolean equals(Object[] a, Object[] a2)`** 
  比较两个对象数组。

#### 2.2.5.6. **填充数组 Arrays.fill**

- **`static void fill(int[] a, int val)`** 
  用 `val` 填充整个数组。
- **`static void fill(int[] a, int fromIndex, int toIndex, int val)`** 
  用 `val` 填充数组的 `[fromIndex, toIndex)` 部分。



# ======

# 3、常用包的使用介绍

## 3.1 Scanner：键盘输入的实现

- 键盘输入代码的四个步骤：
  1. 导包：`import java.util.Scanner;`
  2. 创建Scanner类型的对象：`Scanner scan = new Scanner(System.in);`
  3. 调用Scanner类的相关方法（`next() / nextXxx()`），来获取指定类型的变量
  4. 释放资源：`scan.close();`
- 注意：需要根据相应的方法，来输入指定类型的值。如果输入的数据类型与要求的类型不匹配时，会报异常 导致程序终止。

### 3.1.1 各种类型的数据输入

**案例：**小明注册某交友网站，要求录入个人相关信息。如下：

请输入你的网名、你的年龄、你的体重、你是否单身、你的性别等情况。

```java
//① 导包
import java.util.Scanner;

public class ScannerTest1 {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);//System.in默认代表键盘输入
        
        //③根据提示，调用Scanner的方法，获取不同类型的变量
        System.out.println("欢迎光临你好我好交友网站！");
        System.out.print("请输入你的网名：");
        String name = scanner.next();

        System.out.print("请输入你的年龄：");
        int age = scanner.nextInt();

        System.out.print("请输入你的体重：");
        double weight = scanner.nextDouble();

        System.out.print("你是否单身（true/false)：");
        boolean isSingle = scanner.nextBoolean();

        System.out.print("请输入你的性别：");
        char gender = scanner.next().charAt(0);//先按照字符串接收，然后再取字符串的第一个字符（下标为0）

        System.out.println("你的基本情况如下：");
        System.out.println("网名：" + name + "\n年龄：" + age + "\n体重：" + weight + 
                           "\n单身：" + isSingle + "\n性别：" + gender);
        
        //④ 关闭资源
        scanner.close();
    }
}
```



## 3.2 Math.random：获取随机数

如何产生一个指定范围的随机整数？

1、Math类的random()的调用，会返回一个[0,1)范围的一个double型值

2、Math.random() * 100  --->  [0,100)
      (int)(Math.random() * 100)	---> [0,99]
      (int)(Math.random() * 100) + 5  ----> [5,104]

3、如何获取`[a,b]`范围内的随机整数呢？`(int)(Math.random() * (b - a + 1)) + a`

4、举例

```java
class MathRandomTest {
	public static void main(String[] args) {
		//[1,6]
		int number = (int)(Math.random() * 6) + 1;
		System.out.println(number);
	}
}
```



## 3.3Object 类的使用

### 3.3.1 如何理解根父类

类 `java.lang.Object`是类层次结构的根类，即所有其它类的父类。每个类都使用 `Object` 作为超类。

<img src="http://jason243.online/javase_songhongkang/Object/java005.png" alt="java005.png"/>

- Object类型的变量与除Object以外的任意引用数据类型的对象都存在多态引用

- 所有对象（包括数组）都实现这个类的方法。

- 如果一个类没有特别指定父类，那么默认则继承自Object类。

  

### 3.3.2 Object类的方法

根据JDK源代码及Object类的API文档，Object类当中包含的方法有11个。这里我们主要关注其中的6个：

#### 1、equals()  (重点)

**（1）= =：** 

- 基本类型比较值:只要两个变量的值相等，即为true。

- 引用类型比较引用(是否指向同一个对象)：只有指向同一个对象时，==才返回true。

  - 用“==”进行比较时，符号两边的`数据类型必须兼容`(可自动转换的基本数据类型除外)，**否则编译出错**

**（2）equals()：**所有类都继承了Object，也就获得了equals()方法。还可以重写。

- 只能比较引用类型，**Object类源码中equals()的作用与 “==” 相同**：比较是否指向同一个对象。	 

- `obj1.equals(obj2)`

- 特例：当用equals()方法进行比较时，对类File、String、Date及包装类（Wrapper Class）来说，是比较类型及内容而不考虑引用的是否是同一个对象；

  - 原因：在这些类中重写了Object类的equals()方法。

- 当自定义使用equals()时，可以重写。用于比较两个对象的“内容”是否都相等

  - 任何情况下，x.equals(null)，永远返回是“false”；

    ​    x.equals(和x不同类型的对象)永远返回是“false”。


##### **\*面试题：**`==` 和 `equals` 的区别

> 从我面试的反馈，85%的求职者“理直气壮”的回答错误…

- == 既可以比较基本类型也可以比较引用类型。对于基本类型就是比较值，对于引用类型就是比较内存地址
- equals的话，它是属于java.lang.Object类里面的方法，如果该方法没有被重写过默认也是==；我们可以看到String等类的equals方法是被重写过的，而且String类在日常开发中用的比较多，久而久之，形成了equals是比较值的错误观点。
- 具体要看自定义类里有没有重写Object的equals方法来判断。
- 通常情况下，重写equals方法，会比较类中的相应属性是否都相等。



#### 2、toString()  (重点)

方法签名：public String toString()

① 默认情况下，toString()返回的是“对象的运行时类型 @ 对象的hashCode值的十六进制形式"

② 在进行String与其它类型数据的连接操作时，自动调用toString()方法

```java
Date now=new Date();
System.out.println(“now=” + now);  //相当于
System.out.println(“now=” + now.toString()); 
```

③ 如果我们直接System.out.println(对象)，默认会自动调用这个对象的toString()

④ 可以根据需要在用户自定义类型中重写toString()方法
	如String 类重写了toString()方法，返回字符串的值。

```java
s1 = "hello";
System.out.println(s1);//相当于System.out.println(s1.toString());
```



#### 3、clone()

`clone()` 方法来自于 `Object` 类，默认是一个 **浅拷贝** 方法。

需要实现 **Cloneable 接口**，否则会抛出 `CloneNotSupportedException` 异常。

> 即：如果一个类未实现 `Cloneable` 接口，调用 `clone()` 会抛出 `CloneNotSupportedException`

**浅拷贝**：只复制对象本身及其基本属性（或对引用类型复制引用地址）。

**深拷贝**：除了复制对象本身，还复制引用类型属性所指向的对象（需要手动实现深拷贝）。

```java
class Animal implements Cloneable {
    private String name;
    private int[] favoriteNumbers; // 引用类型字段

    // 省略代码

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // Obeject实现的是浅拷贝
    }

public class ShallowCopyTest {
    public static void main(String[] args) throws CloneNotSupportedException {
        int[] numbers = {1, 2, 3};
        Animal a1 = new Animal("花花", numbers);
        Animal a2 = (Animal) a1.clone();

        // 修改克隆对象的引用类型字段
        a2.getFavoriteNumbers()[0] = 100;	// 下面的输出，100跟着一起改了，因为是浅拷贝
        a2.setName("朵朵");	// 下面的输出，原始对象还是花花，这个与 String 的底层实现有关，String是不可变的，这里事实上是在 字符串常量池 中new了一个"朵朵"，然后将引用赋值给了 a2.name，没有改动原来a2.name和a1.name指向的 "花花" 所在地址的值。 

        System.out.println("原始对象：" + a1);
        System.out.println("克隆对象：" + a2);
    }
}
```

打印结果

<img src="http://jason243.online/javase_songhongkang/Object/java004.png" alt="java004.png"/>





#### 4、finalize()

- 当对象被回收时，finalizer线程会调用该对象的 finalize() 方法。
- 什么时候被回收：当某个对象没有任何引用时，JVM就认为这个对象是垃圾对象，就会在之后不确定的时间使用垃圾回收机制来销毁该对象，在销毁该对象前，会先调用 finalize()方法。 
- 子类可以重写该方法，目的是在对象被清理之前执行必要的清理操作。比如，在方法内断开相关连接资源。
  - 如果重写该方法，让一个新的引用变量重新引用该对象，则会重新激活对象。
- 在JDK 9中此方法已经被`标记为过时`的。



#### 5、getClass()

public final Class<?> getClass()：获取对象的运行时类型

> 因为Java有多态现象，所以一个引用数据类型的变量的编译时类型与运行时类型可能不一致，因此如果需要查看这个变量实际指向的对象的类型，需要用getClass()方法

```java
public static void main(String[] args) {
	Object obj = new Person();
	System.out.println(obj.getClass());//运行时类型
}
```

结果：

```java
class com.atguigu.java.Person
```



#### 6、hashCode()

public int hashCode()：返回每个对象的hash值。(后续在集合框架章节重点讲解)

```java
public static void main(String[] args) {
	System.out.println("AA".hashCode());//2080
    System.out.println("BB".hashCode());//2112
}
```









======

# 4、其他补充

## 4.1 **可变参数（Variable Arguments）简介**

在Java中，可变参数允许方法接受**不固定数量**的参数。可变参数在方法定义时使用省略号`...`表示。

---

### 4.1.1、**特点详解**

#### **（1）参数个数可变**
- **定义**：可变参数可以接收 **0个、1个或多个参数**。
- **语法**：通过在数据类型后加`...`来定义可变参数。例如：
  ```java
  public void printNumbers(int... numbers) {
      for (int number : numbers) {
          System.out.println(number);
      }
  }
  ```
  调用方法时，可以传入0个、1个或多个`int`参数：
  ```java
  printNumbers(); // 不传参数
  printNumbers(1); // 传入1个参数
  printNumbers(1, 2, 3); // 传入多个参数
  ```

---

#### **（2）与同名方法构成重载**

> 有关重载的面试时重要考点：**说明 `重载(Overloading)` 和 `重写/覆盖(Override)` 的区别**
>
> 他们是多态的三种表现形式之二（还有一个对象的多态）
>
> - 重载 是编译时多态（静态多态），表现为同一个类中有多个同名方法但是参数不同
> - 重写/覆盖 是运行时多态（动态多态），表现为子类继承时重写父类的方法
>
> 面向对象的三个特征：封装、继承、多态

- **定义**：如果一个类中有多个方法名称相同，但参数类型或数量不同，可变参数方法与其他同名方法会构成**方法重载**。
- **示例**：
  ```java
  public void print(String message) {
      System.out.println("Single argument: " + message);
  }

  public void print(String... messages) {
      for (String message : messages) {
          System.out.println("Multiple arguments: " + message);
      }
  }
  ```
  调用时：
  ```java
  print("Hello"); // 调用第一个方法
  print("Hello", "World"); // 调用第二个方法（可变参数）
  ```

---

#### **（3）不可同时使用数组和可变参数**
- **规则**：在同一个方法中，不能同时使用数组和可变参数，否则会报错。
- **示例**（错误写法）：
  
  ```java
  public void testMethod(int[] arr, int... nums) {
      // 报错：不能同时声明数组和可变参数
  }
  ```
  **原因**：可变参数在底层实际上是以**数组形式**实现的，因此数组与可变参数不能同时声明，会造成歧义。

---

#### **（4）可变参数必须是最后一个参数**
- **规则**：在方法参数中，可变参数必须是**最后一个参数**，否则会报错。
- **示例**：
  
  ```java
  // 正确写法：
  public void printData(String name, int... data) { 
      // do something
}
  
  // 错误写法（可变参数不是最后一个参数）：
  public void printData(int... data, String name) { 
      // 编译错误
  }
  ```

---

#### **（5）只能声明一个可变参数**
- **规则**：在一个方法中，最多只能有一个可变参数，不能有多个可变参数。
- **示例**（错误写法）：
  
  ```java
  public void testMethod(int... nums1, int... nums2) {
      // 报错：方法参数中不能有多个可变参数
  }
  ```

---

### 4.1.2、**可变参数的底层实现**
- **数组实现**：Java底层会将传入的可变参数转换为一个数组。例如：
  ```java
  public void test(int... nums) {
      System.out.println(nums.length); // 可变参数底层为数组
  }
  test(1, 2, 3); // nums 等同于 int[] nums = {1, 2, 3};
  ```

---

### 4.1.3、**总结**
1. 可变参数允许接收任意数量的参数，包括0个。
2. 与同名方法构成重载，方法调用时根据参数的数量或类型匹配合适的方法。
3. 可变参数底层是数组，因此不能同时使用数组和可变参数。
4. 可变参数必须声明为方法参数列表的最后一个参数。
5. 在一个方法中，最多只能声明一个可变参数。



## 4.2、**JavaBean**

JavaBean 是 Java 语言中一种用于封装数据和实现可重用功能的组件类，它的设计目的是使 Java 对象的属性和行为可以通过工具（例如 GUI 编辑器）方便地访问和修改。

---

### 4.2.1. **JavaBean 的定义**
   - **JavaBean 是什么？**
     JavaBean 是一种符合特定规则的 Java 类，用于封装数据、提供功能，并可以被其他开发工具或程序复用。

---

### 4.2.2. **JavaBean 的标准**
一个类如果要被称为 JavaBean，需要符合以下规则：
   - **类是公共的**：
     - 类必须用 `public` 修饰，这样才能在包外被其他程序访问。
     
   - **必须有一个无参的公共构造器**：
     - 无参构造器是必须的，因为许多工具（例如框架或 IDE）会通过反射机制创建 JavaBean 实例，而反射需要无参构造器。
     
   - **属性必须是私有的，且有对应的 `get` 和 `set` 方法**：
     - 属性设置为私有，保证封装性。
     - 通过 `get` 和 `set` 方法公开属性的访问和修改接口。

---

### 4.2.3. **JavaBean 的作用**
   - **封装数据和功能**：
     - JavaBean 可以用来存储对象的数据，并通过 `get` 和 `set` 方法访问和修改。
   - **与其他 Java 技术集成**：
     - JavaBean 经常与 JSP、Servlet 等技术结合，用于数据传递和显示。
     - 例如，在 JSP 页面中，可以通过 JavaBean 获取数据库的数据并动态显示。
   - **支持工具操作**：
     - JavaBean 的标准化设计，使得许多开发工具可以直接识别它，并通过图形化界面操作其属性。

---

### 4.2.4. **JavaBean 的实际应用**
   - **图形界面组件**：
     - 最初 JavaBean 是为 GUI（例如按钮、复选框等组件）设计的。
     - IDE 会帮助创建这些组件的 Java 类，并将它们的属性通过 `get` 和 `set` 方法暴露出来，供开发者修改。

   - **Web 开发**：
     - 在 Web 开发中，JavaBean 经常用作数据模型，负责在前端（如 JSP 页面）和后端（如 Servlet）之间传递数据。

---

### 4.2.5. **示例：一个简单的 JavaBean**
以下是一个符合 JavaBean 标准的类：

```java
public class Person {
    private String name;  // 私有属性
    private int age;      // 私有属性

    // 无参构造器
    public Person() {
    }

    // 有参构造器（可选，不是 JavaBean 的必要条件）
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // get 方法
    public String getName() {
        return name;
    }

    // set 方法
    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

使用这个 JavaBean 类：

```java
public class Main {
    public static void main(String[] args) {
        Person person = new Person(); // 调用无参构造器
        person.setName("张三");       // 使用 set 方法赋值
        person.setAge(25);

        System.out.println(person.getName()); // 使用 get 方法获取值
        System.out.println(person.getAge());
    }
}
```

---

### 4.2.6. 总结
JavaBean 是一种遵循特定规则的 Java 类，主要特点是封装数据、提供无参构造器和 `get`/`set` 方法。它广泛应用于 GUI 和 Web 开发，帮助开发者更方便地传递和处理数据。



## 4.3、注解

在 Java 代码中，方法上一行加的 `@xxxxx` 属于**注解（Annotation）**。注解是 Java 提供的一种**元数据**形式，用于为代码提供附加信息，可以作用于类、方法、字段、参数等。

---

### 4.3.1、**什么是注解？**
1. **注解（Annotation）** 是一种修饰符，可以在编译时或运行时为程序提供元数据。
2. 注解的本质是一个特殊的接口，注解类型的定义使用 `@interface` 关键字。

---

### 4.3.2、**注解的作用**
注解的主要功能有以下几类：
1. **编译器指令**：
   - 提供信息给编译器，避免编译错误或警告。
2. **代码生成**：
   - 注解可以与工具或框架结合，用于自动生成代码。
3. **运行时行为**：
   - 注解可以在运行时被反射机制（Reflection）读取并影响程序逻辑。

---

### 4.3.3、**常见的注解**
以下是一些常见的 Java 注解及其功能：

#### **4.3.3.1 编译器相关的注解**
这些注解主要用于提示编译器执行特定的检查或行为：
- `@Override` 
  指示当前方法重写了父类的方法。
  
  - 用于检测被标记的方法为有效的重写方法，如果不是，则报编译错误！
  
  - 只能标记在方法上。
  
  - 它会被编译器程序读取。
  
- `@Deprecated` 
  标记某个方法或类已过时，不建议使用。
  
  - 用于表示被标记的数据已经过时，不推荐使用。
  
  - 可以用于修饰 属性、方法、构造、类、包、局部变量、参数。
  
  - 它会被编译器程序读取。
  
- `@SuppressWarnings` 
  抑制编译器警告。
  
  - 抑制编译警告。当我们不希望看到警告信息的时候，可以使用 SuppressWarnings 注解来抑制警告信息
  
  - 可以用于修饰类、属性、方法、构造、局部变量、参数
  
  - 它会被编译器程序读取。

---

#### **4.3.3.2 运行时相关的注解**
这些注解通常与框架（如 Spring、Hibernate 等）结合使用，用于改变运行时行为：
- `@Entity` 
  用于标记一个类为数据库实体类（通常在 Hibernate 中使用）。
  
- `@Autowired` 
  用于依赖注入（通常在 Spring 中使用）。
  
- `@RequestMapping` 
  在 Spring MVC 中，用于映射 HTTP 请求到控制器方法。

---

#### **4.3.3.3 自定义注解**
开发者可以根据需要定义自己的注解。

**示例：定义和使用自定义注解**
```java
// 定义注解
import java.lang.annotation.*;

@Retention(RetentionPolicy.RUNTIME) // 保留策略
@Target(ElementType.METHOD)         // 目标位置
public @interface MyAnnotation {
    String value() default "Default Value";
}

// 使用注解
class Test {
    @MyAnnotation(value = "Hello, Annotation!") // 使用自定义注解
    public void testMethod() {
        System.out.println("This is a test method");
    }
}

// 通过反射读取注解
import java.lang.reflect.Method;

public class Main {
    public static void main(String[] args) throws Exception {
        Method method = Test.class.getMethod("testMethod");
        MyAnnotation annotation = method.getAnnotation(MyAnnotation.class);
        System.out.println(annotation.value()); // 输出：Hello, Annotation!
    }
}
```

---

### 4.3.4、**注解的核心部分**
1. **元注解（Meta-Annotation）**
   - Java 提供了几种特殊的注解，用于定义其他注解的行为：
     - `@Retention`：定义注解的生命周期（源码、字节码或运行时）。
     - `@Target`：定义注解的作用范围（类、方法、字段等）。
     - `@Documented`：表示注解会包含在生成的 JavaDoc 中。
     - `@Inherited`：表示注解可以被子类继承。

2. **注解的生命周期**
   - `SOURCE`：只在源码中存在，编译后消失。
   - `CLASS`：在字节码中存在，但运行时不可用（默认）。
   - `RUNTIME`：在运行时也可以通过反射获取。

### 4.3.5、常见的Annotation作用

**示例1：生成文档相关的注解**

```java
@author 标明开发该类模块的作者，多个作者之间使用,分割
@version 标明该类模块的版本
@see 参考转向，也就是相关主题
@since 从哪个版本开始增加的
@param 对方法中某参数的说明，如果没有参数就不能写
@return 对方法返回值的说明，如果方法的返回值类型是void就不能写
@exception 对方法可能抛出的异常进行说明 ，如果方法没有用throws显式抛出的异常就不能写
```

**示例2：在编译时进行格式检查(JDK内置的三个基本注解)**

`@Override`: 限定重写父类方法，该注解只能用于方法

`@Deprecated`: 用于表示所修饰的元素(类，方法等)已过时。通常是因为所修饰的结构危险或存在更好的选择

`@SuppressWarnings`: 抑制编译器警告

**示例3：跟踪代码依赖性，实现替代配置文件功能**

- Servlet3.0提供了注解(annotation)，使得不再需要在web.xml文件中进行Servlet的部署。

- Spring框架中关于“事务”的管理



# =====

# 5、泛型(Generic)

## 1.认识泛型

泛型就是给方法或类接收的数据类型作说明，保证java的类型安全



## 2. 使用泛型举例

### 2.1 集合中使用泛型

**集合中使用泛型时：**

<img src="http://jason243.online/javase_songhongkang/Generic/java001.png" alt="image-20220411001549747" style="zoom:80%;" />

> Java泛型可以保证如果程序在编译时没有发出警告，运行时就不会产生ClassCastException异常。即，把不安全的因素在编译期间就排除了，而不是运行期；既然通过了编译，那么类型一定是符合要求的，就避免了类型转换。
>
> 同时，代码更加简洁、健壮。
>
> **把一个集合中的内容限制为一个特定的数据类型，这就是generic背后的核心思想。**



### 2.2 比较器中使用泛型

```java
package com.atguigu.generic;

import java.util.Comparator;

class CircleComparator1 implements Comparator<Circle> {	//实现泛型

    @Override
    public int compare(Circle o1, Circle o2) {
        //不再需要强制类型转换，代码更简洁
        return Double.compare(o1.getRadius(), o2.getRadius());
    }
}

//测试类
public class TestHasGeneric {
    public static void main(String[] args) {
        CircleComparator1 com = new CircleComparator1();
        System.out.println(com.compare(new Circle(1), new Circle(2)));

        //System.out.println(com.compare("圆1", "圆2"));
        //编译错误，因为"圆1", "圆2"不是Circle类型，是String类型，编译器提前报错，
        //而不是冒着风险在运行时再报错。
    }
}
```



### 2.3 相关使用说明

- 在创建集合对象的时候，可以指明泛型的类型。

  具体格式为：

  ```java
  List<Integer> list = new ArrayList<Integer>();
  
  List<Integer> list = new ArrayList<>(); //类型推断
  ```

- 泛型，也称为泛型参数，即参数的类型，只能使用引用数据类型进行赋值。（不能使用基本数据类型，可以使用包装类替换）

- 集合声明一旦指明泛型，类或接口内部，凡是使用泛型参数的位置，都指定为具体的参数类型。如果没有指明的话，看做是Object类型。



## 3. 自定义泛型结构

### 3.1 泛型的基础说明

**1、<类型>这种语法形式就叫泛型。**

- <类型>的形式我们称为类型参数，这里的"类型"习惯上使用T表示，是Type的缩写。即：<T>。
- <T>：代表未知的数据类型，我们可以指定为<String>，<Integer>，<Circle>等。

**2、在哪里可以声明类型变量\<T>**

- 声明类或接口时，在类名或接口名后面声明泛型类型，我们把这样的类或接口称为`泛型类`或`泛型接口`。

```java
【修饰符】 class 类名<类型变量列表> 【extends 父类】 【implements 接口们】{
    
}
【修饰符】 interface 接口名<类型变量列表> 【implements 接口们】{
    
}

//例如：
public class ArrayList<E>    
public interface Map<K,V>{
    ....
}    
```

- 声明方法时，在【修饰符】与返回值类型之间声明类型变量，我们把声明了类型变量的方法，称为泛型方法。

```java
[修饰符] <类型变量列表> 返回值类型 方法名([形参列表])[throws 异常列表]{
    //...
}

//例如：java.util.Arrays类中的
public static <T> List<T> asList(T... a){
    ....
}
```

### 3.2 自定义泛型类或泛型接口

当我们在类或接口中定义某个成员时，该成员的相关类型是不确定的，而这个类型需要在使用这个类或接口时才可以确定，那么我们可以使用泛型类、泛型接口。

#### 3.2.1 说明

1. **定义泛型后，类的内部（属性、方法、构造器等）可以使用泛型**  

   ```java
   public class Box<T> { // 定义泛型类 Box，T 是类型参数
       private T value; // 属性使用泛型 T
   
       public Box(T value) { // 构造器使用泛型 T
           this.value = value;
       }
   
       public T getValue() { // 方法返回值使用泛型 T
           return value;
       }
   }
   
   // 使用示例
   Box<Integer> intBox = new Box<>(123); // T 被替换为 Integer
   System.out.println(intBox.getValue()); // 输出：123
   ```

2. **如果不指定泛型类型，默认为 Object，但不建议这样使用**  

   ```java
   Box box = new Box("String Value"); // 未指定泛型，默认为 Object
   System.out.println(box.getValue()); // 输出：String Value
   ```

3. **泛型只能使用引用数据类型，不能使用基本数据类型**  

4. **子类继承或实现泛型类时，可以指定具体类型，也可以继续保留泛型**  

   ```java
   // 子类保留泛型
   public class GenericSubClass<T> extends Box<T> {
       public GenericSubClass(T value) {
           super(value);
       }
   }
   
   // 子类指定具体类型
   public class StringBox extends Box<String> {
       public StringBox(String value) {
           super(value);
       }
   }
   
   GenericSubClass<Integer> genericSubClass = new GenericSubClass<>(100);
   System.out.println(genericSubClass.getValue()); // 输出：100
   
   StringBox stringBox = new StringBox("Hello");
   System.out.println(stringBox.getValue()); // 输出：Hello
   ```



#### 3.2.2 注意

1. **泛型可以有多个参数** 

**示例**：

```java
   public class Pair<K, V> { // 定义泛型类，K 和 V 是两个类型参数
       private K key;
       private V value;
   
       public Pair(K key, V value) {
           this.key = key;
           this.value = value;
       }
   
       public K getKey() {
           return key;
       }
   
       public V getValue() {
           return value;
       }
   }
   
   // 使用 Pair 类
   Pair<String, Integer> pair = new Pair<>("Age", 25);
   System.out.println(pair.getKey() + ": " + pair.getValue()); // 输出：Age: 25
```

2. **JDK 7+ 支持泛型推断** 

   ```java
   List<String> list = new ArrayList<>(); // 类型推断，省略右侧的 <String>
   ```

3. **不能直接创建泛型数组，但可以用类型转换实现** 

   **示例**：

   参考：ArrayList源码中声明：Object[] elementData，而非泛型参数类型数组。

   ```java
   // 错误：不能直接 new 泛型数组
   // T[] array = new T[10]; 
   
   // 正确：通过 Object 转型
   Object[] objArray = new Object[10];
   Integer[] intArray = (Integer[]) objArray;
   
   ```

4. **异常类不能是泛型的** 

   **示例**：

   ```java
   // 错误：泛型类不能继承 Throwable
   // public class MyException<T> extends Exception {}
   
   // 正确：使用具体类型定义异常类
   public class MyException extends Exception {
       public MyException(String message) {
           super(message);
       }
   }
   ```

5. **不可以在静态方法中使用类的泛型**

   **原因**：
   静态方法在类加载时就已经存在，与类的实例无关，而类的泛型是在创建实例时具体化的。因此，静态方法无法使用类级别的泛型参数。



### 3.3 自定义泛型方法

如果我们定义类、接口时没有使用<泛型参数>，但是某个方法形参类型不确定时，这个方法可以单独定义<泛型参数>。

#### 3.3.1 说明

- 泛型方法的格式：

```java
[访问权限]  <泛型>  返回值类型  方法名([泛型标识 参数名称])  [抛出的异常]{
    
}
```

- 方法，也可以被泛型化，与其所在的类是否是泛型类没有关系。
- 泛型方法中的泛型参数在方法被调用时确定。
- 泛型方法可以根据需要，声明为static的。

#### 3.3.2 举例

```java
public class DAO {

    public <E> E get(int id, E e) {

        E result = null;

        return result;
    }
}
```



## 4. 泛型在继承上的体现

如果B是A的一个子类型（子类或者子接口），而G是具有泛型声明的类或接口，G\<B>并不是G\<A>的子类型！

比如：String是Object的子类，但是List\<String>并不是List\<Object>的子类。

<img src="http://jason243.online/javase_songhongkang/Generic/java002.png" alt="java002" style="zoom:67%;" />

```java
public void testGenericAndSubClass() {
    Person[] persons = null;
    Man[] mans = null;
    //Person[] 是 Man[] 的父类
    persons = mans;

    Person p = mans[0];

    // 在泛型的集合上
    List<Person> personList = null;
    List<Man> manList = null;
    //personList = manList;(报错)
}
```



## 5. 通配符的使用

当我们声明一个变量/形参时，这个变量/形参的类型是一个泛型类或泛型接口，例如：Comparator\<T>类型，但是我们仍然无法确定这个泛型类或泛型接口的类型变量\<T>的具体类型，此时我们考虑使用类型通配符  `?` 。

### 5.1 通配符的理解

使用类型通配符：？ 

比如：`List<?>`，`Map<?,?>`

​            `List<?>`是`List<String>`、`List<Object>`等各种泛型List的父类。



### 5.2 通配符的读与写

**写操作：**

将任意元素加入到其中不是类型安全的：

```java
Collection<?> c = new ArrayList<String>();

c.add(new Object()); // 编译时错误
```

**泛型的实际存储类型是未知的**

- 当你声明一个 `Collection<?> c = new ArrayList<String>();` 时：
  - `c` 的实际存储类型是 `ArrayList<String>`。
  - 编译器只知道 `c` 是一个 `Collection`，但不知道它的具体元素类型是什么。

**对于 `Collection<?>`，`E` 是一个未知类型（`?`）。**

- 编译器不知道 `E` 具体是什么类型，所以任何非 `null` 值都可能不符合集合的实际类型要求。
- **因此，编译器禁止任何写操作**，避免潜在的类型不匹配。

唯一可以插入的元素是null，因为它是所有引用类型的默认值。



**读操作：**

另一方面，读取List<?>的对象list中的元素时，永远是安全的，因为不管 list 的真实类型是什么，它包含的都是Object。

```java
public static void main(String[] args) {
    List<?> list = null;
    list = new ArrayList<String>();
    list = new ArrayList<Double>();
    // list.add(3);//编译不通过
    list.add(null);

    List<String> l1 = new ArrayList<String>();
    List<Integer> l2 = new ArrayList<Integer>();
    l1.add("尚硅谷");
    l2.add(15);
    read(l1);
    read(l2);
}

public static void read(List<?> list) {
    for (Object o : list) {
        System.out.println(o);
    }
}
```



### 5.3 使用注意点

注意点1：编译错误：不能用在泛型方法声明上，返回值类型前面<>不能使用"?"

```java
/*
	public static <?> void test(ArrayList<?> list){
	
	}
*/
```

注意点2：编译错误：不能用在泛型类的声明上

```java
/*
	class GenericTypeClass<?>{

	}
*/
```

注意点3：编译错误：不能用在创建对象上，右边属于创建集合对象

```java
//	ArrayList<?> list2 = new ArrayList<?>();
```



### 5.4 有限制的通配符

- `<?>`

  - 允许所有泛型的引用调用

- 通配符指定上限：`<? extends 类/接口 >`

  - 使用时指定的类型必须是继承某个类（子类），或者实现某个接口，即<= 

- 通配符指定下限：`<? super 类/接口 >`

  - 使用时指定的类型必须是操作的类或接口，或者是操作的类的父类或接口的父接口，即>=

- 说明：

  ```java
  <? extends Number>     //(无穷小 , Number]
  //只允许泛型为Number及Number子类的引用调用
  
  <? super Number>      //[Number , 无穷大)
  //只允许泛型为Number及Number父类的引用调用
  
  <? extends Comparable>
  //只允许泛型为实现Comparable接口的实现类的引用调用
  ```



### **5.4.1 `<? extends T>`：指定上限**

**含义**

- `? extends T` 表示泛型类型是 `T` 或 `T 的子类`。
- 它的目的是限制一个泛型可以接受的类型，确保类型是 **T 或更小的范围**（子类）。

**特点**

- **只能读取，不允许写入**（除了 `null`）。
- 使用这种边界时，你可以安全地读取集合中的元素，知道它们是 `T` 或 `T` 的子类，但不能向集合中写入元素，因为无法确定具体的子类型。

**类比**

把 `<? extends T>` 想象为一个窗口，只能看，但不能放东西。

**例子**

```java
public void printNumbers(List<? extends Number> list) {
    for (Number num : list) {
        System.out.println(num);
    }
}

// 以下均合法：
printNumbers(new ArrayList<Integer>()); // Integer 是 Number 的子类
printNumbers(new ArrayList<Double>());  // Double 是 Number 的子类

```

- `list` 的泛型类型必须是 `Number` 或 `Number` 的子类（如 `Integer`、`Double`）。
- 你可以安全地读取 `Number` 或其子类的值。

**但你不能写入**，例如：

```java
list.add(new Integer(5)); // 编译错误，泛型类型未知
```

原因是：`list` 可能是 `ArrayList<Double>`，向其中添加 `Integer` 是不安全的。



### **5.4.2 `<? super T>`：指定下限**

**含义**

- `? super T` 表示泛型类型是 `T` 或 `T 的父类`。
- 它的目的是限制一个泛型可以接受的类型，确保类型是 **T 或更大的范围**（父类）。

**特点**

- **允许写入，限制读取**。
- 你可以向集合中添加类型为 `T` 或其子类的元素，但读取时只能保证返回 `Object` 类型，因为父类范围可能过于宽泛。

**类比**

把 `<? super T>` 想象为一个容器，可以放东西，但取出来的内容可能不知道具体类型。

**例子**

```java
public void addNumbers(List<? super Integer> list) {
    list.add(5); // 合法，Integer 是 Integer 或其子类
    list.add(new Integer(10)); // 合法
}

// 以下均合法：
addNumbers(new ArrayList<Integer>());   // Integer 是 Integer 本身
addNumbers(new ArrayList<Number>());    // Number 是 Integer 的父类
addNumbers(new ArrayList<Object>());    // Object 是 Number 的父类
```

- `list` 的泛型类型必须是 `Integer` 或 `Integer` 的父类（如 `Number`、`Object`）。
- 你可以向 `list` 中添加 `Integer`，因为它的范围保证兼容。

**但你不能安全读取**，例如：

```java
Integer num = list.get(0); // 编译错误，泛型类型不确定
Object obj = list.get(0);  // 合法，只能读取为 Object

```

原因是：`list` 可能是 `ArrayList<Object>`，返回的内容可能只是 `Object` 类型。

### **5.4.3 总结对比**

| **通配符**      | **含义**                | **可读性**              | **可写性**                  | **典型用途**                                     |
| --------------- | ----------------------- | ----------------------- | --------------------------- | ------------------------------------------------ |
| `<? extends T>` | 泛型必须是 `T` 或其子类 | **可以读取为 `T`**      | **不能写入（除了 `null`）** | 只需从集合中读取数据时，常用于生产者（Producer） |
| `<? super T>`   | 泛型必须是 `T` 或其父类 | **只能读取为 `Object`** | **可以写入 `T` 或其子类**   | 需要向集合中添加数据时，常用于消费者（Consumer） |

### **5.4.4 常见记忆法**

- **`extends`（上限）**：你只知道类型是 `T` 或更窄（子类），所以只能安全读取，无法写入。
- **`super`（下限）**：你只知道类型是 `T` 或更宽（父类），所以可以安全写入 `T` 或其子类，但读取的类型只能保证是 `Object`。