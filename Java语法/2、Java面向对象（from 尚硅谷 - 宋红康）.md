# Java面向对象

# 1、面向对象基础（面向对象三要素）

## 1.1、this与super

### 1.1.1 this

#### 1.1.1.1 实例方法或构造器中使用当前对象的成员

<img src="http://jason243.online/javase_songhongkang/Object/java002.png" alt="image-20220503102947013" style="zoom:67%;" />

**使用this访问属性和方法时，如果在本类中未找到，会从父类中查找。这个在继承中会讲到。**



#### 1.1.1.2 同一个类中构造器互相调用

this可以作为一个类中构造器相互调用的特殊格式。

- this()：调用本类的无参构造器
- this(实参列表)：调用本类的有参构造器

```java
public class Student {
    private String name;
    private int age;

    // 无参构造
    public Student() {
//        this("",18);//调用本类有参构造器
    }

    // 有参构造
    public Student(String name) {
        this();//调用本类无参构造器
        this.name = name;
    }
    // 有参构造
    public Student(String name,int age){
        this(name);//调用本类中有一个String参数的构造器
        this.age = age;
    }

    public String getInfo(){
        return "姓名：" + name +"，年龄：" + age;
    }
}
```

注意：

- 不能出现递归调用。比如，调用自身构造器。
  - 推论：如果一个类中声明了n个构造器，则最多有 n - 1个构造器中使用了"this(形参列表)"
- **this()和this(实参列表)只能声明在构造器首行。**
  - 推论：在类的一个构造器中，最多只能声明一个"this(参数列表)"，也就是只能使用this调用一次另一个构造器。



### 1.1.2 super

#### 1.1.2.1 super与this参与下的就近原则

- **方法前面没有super.和this.**
  - 先从子类找匹配方法，如果没有，再从直接父类找，再没有，继续往上追溯
- **方法前面有this.**
  - 先从子类找匹配方法，如果没有，再从直接父类找，再没有，继续往上追溯
- **方法前面有super.**
  - 从当前子类的直接父类找，如果没有，继续往上追溯



#### 1.1.2.2 子类构造器中调用父类构造器

① 子类继承父类时，不会继承父类的构造器。只能通过“super(形参列表)”的方式调用父类指定的构造器。

② 规定：“super(形参列表)”，必须声明在构造器的首行。

③ 我们前面讲过，在构造器的首行可以使用"this(形参列表)"，调用本类中重载的构造器，
     结合②，结论：在构造器的首行，**"this(形参列表)" 和 "super(形参列表)"只能二选一**。

④ 如果在子类构造器的首行既没有显示调用"this(形参列表)"，也没有显式调用"super(形参列表)"，则子类此构造器默认调用"super()"，即调用父类中空参的构造器。





## 1.2、封装（Encapsulation）

<img src="http://jason243.online/javase_songhongkang/Object/java001.png" style="zoom:67%;"/>



## 1.3、继承（Inheritance）

### 1.3.1 继承中的基本概念

- 通过 `extends` 关键字，可以声明一个类B继承另外一个类A

- 类B，称为子类、派生类(derived class)、SubClass

- 类A，称为父类、超类、基类(base class)、SuperClass



### 1.3.2 继承的细节说明

**1、子类会继承父类所有的实例变量和实例方法**

- 当子类对象调用方法时，编译器会先在子类模板中看该类是否有这个方法，如果没找到，会看它的父类甚至父类的父类是否声明了这个方法，遵循`从下往上`找的顺序，找到了就停止，一直到根父类都没有找到，就会报编译错误。

所以继承意味着子类的对象除了看子类的类模板还要看父类的类模板。

**2、子类不能直接访问父类中私有的(private)的成员变量和方法**

子类虽会继承父类私有(private)的成员变量，但子类不能对继承的私有成员变量直接进行访问

**3、在Java 中，继承的关键字用的是“extends”，即子类不是父类的子集，而是对父类的“扩展”**

**4、Java支持多层继承(继承体系)**

**5、一个父类可以同时拥有多个子类**

**6、Java只支持单继承，不支持多重继承**



## 1.4、多态（Polymorphism）

### 1.4.1、对象的多态性

多态性，是面向对象中最重要的概念

**对象的多态性：父类的引用指向子类的对象**

```java
Person p = new Student();

Object o = new Person();//Object类型的变量o，指向Person类型的对象

o = new Student(); //Object类型的变量o，指向Student类型的对象
```

对象的多态：在Java中，子类的对象可以替代父类的对象使用。所以，一个引用类型变量可能指向(引用)多种不同类型的对象

#### 1.4.1.1 多态的理解

Java引用变量有两个类型：`编译时类型`和`运行时类型`。编译时类型由`声明`该变量时使用的类型决定，运行时类型由`实际赋给该变量的对象`决定。简称：**编译时，看左边；运行时，看右边。**

- 若编译时类型和运行时类型不一致，就出现了对象的多态性(Polymorphism)
- 多态情况下，“看左边”：看的是父类的引用（父类中不具备子类特有的方法）
      “看右边”：看的是子类的对象（实际运行的是子类重写父类的方法）

多态的使用前提：① 类的继承关系  ② 方法的重写

#### 1.4.1.2 多态的好处和弊端

**好处**：变量引用的子类对象不同，执行的方法就不同，实现**动态绑定**。**代码编写更灵活、功能更强大，可维护性和扩展性更好了**。

**弊端**：一个引用类型变量如果声明为父类的类型，但实际引用的是子类对象，那么该变量就**不能再访问子类中添加的属性和方法**。

```java
Student m = new Student();
m.school = "pku"; 	//合法,Student类有school成员变量
Person e = new Student(); 
e.school = "pku";	//非法,Person类没有school成员变量

// 属性是在编译时确定的，编译时e为Person类型，没有school成员变量，因而编译错误。
```

> 解决方案：
> 向下转型（Downcasting） ，但需配合 instanceof 检查以避免 ClassCastException。
>
> ```java
>   if (animal instanceof Dog) {
>       Dog dog = (Dog) animal;
>       dog.bark();  // 安全调用
>   }
> ```



#### 1.4.1.3 成员变量没有多态性

- 若子类重写了父类方法，就意味着子类里定义的方法彻底覆盖了父类里的同名方法，系统将不可能把父类里的方法转移到子类中。
- 对于实例变量则不存在这样的现象，即使子类里定义了与父类完全相同的实例变量，这个实例变量依然不可能覆盖父类中定义的实例变量

因为成员变量没有多态性，所以**对成员变量的调用采用静态链接（早期绑定）**，即调用编译时类型对象的成员变量。相关概念的解释见下面4.4.1.4。



#### 1.4.1.4 虚方法、对象的运行时类型与编译时类型、向上转型与向下转型

#### （1）虚方法调用(Virtual Method Invocation)

在Java中虚方法是指在编译阶段不能确定方法的调用入口地址，在运行阶段才能确定的方法，即可能被重写的方法。

```java
Person e = new Student();
e.getInfo();	// 调用Student类的getInfo()方法，此时称父亲的方法为虚方法。
				// 同时，这种多态调用只允许调用父类中声明的成员方法，子类额外实现的方法不允许调用
```

子类中定义了与父类同名同参数的方法，在多态情况下，将此时父类的方法称为虚方法，父类根据赋给它的不同子类对象，动态调用属于子类的该方法。这样的方法调用在编译期是无法确定的。

> 拓展：
>
> `静态链接（或早期绑定）`：当一个字节码文件被装载进JVM内部时，如果被调用的目标方法在编译期可知，且运行期保持不变时。这种情况下将调用方法的符号引用转换为直接引用的过程称之为静态链接。那么调用这样的方法，就称为非虚方法调用。比如调用静态方法、私有方法、final方法、父类构造器、本类重载构造器等。
>
> `动态链接（或晚期绑定）`：如果被调用的方法在编译期无法被确定下来，也就是说，只能够在程序运行期将调用方法的符号引用转换为直接引用，由于这种引用转换过程具备动态性，因此也就被称之为动态链接。调用这样的方法，就称为虚方法调用。比如调用重写的方法（针对父类）、实现的方法（针对接口）。



#### （2）对象的运行时类型与编译时类型

**1. 对象的运行时类型**

- **运行时类型**指的是对象在运行时实际创建的类型。
- 比如，`new Student()` 创建的对象，它的运行时类型就是 `Student`，不管之后用什么类型的变量引用它，这个运行时类型始终是 `Student`。

**2. 编译时类型**

- ##### **编译时类型**指的是在代码编译时，变量声明的类型。

- 比如：

  ```java
  Person person = new Student();
  ```

  - `person` 的编译时类型是 `Person`（左侧声明的类型）。
  - 但它的运行时类型是 `Student`（右侧 `new` 创建的对象类型）。

**3. 对比**

1. **运行时类型**：对象的本质类型，在程序运行时确定，不会改变。
   - 比如，`new Student()` 的运行时类型是 `Student`。
2. **编译时类型**：变量声明时的类型，在程序编译时确定。
   - 比如，`Person person` 的编译时类型是 `Person`。



#### （3）向上转型与向下转型

1. **向上转型**：将子类对象赋值给父类变量（安全、自动完成）。
   - 编译时只能调用父类中声明的方法，运行时实际调用子类的实现。
2. **向下转型**：将父类变量强制转换为子类类型（可能失败，需要手动完成）。
   - 如果父类变量的实际运行时类型不是目标子类，会抛出 `ClassCastException`。



### 1.4.2、方法的重载——编译时多态

#### 1.4.2.1 方法重载：

- 在同一个类中，允许存在一个以上的同名方法，只要它们的**参数列表不同**即可。

#### 1.4.2.3 重载方法调用：

- JVM 通过方法的参数列表，调用匹配的方法。
  1. **先找个数、类型匹配的**。
  2. **再找个数和类型可以兼容的**，如果没有完全匹配的方法，但有多个方法可以兼容，且 JVM 无法判断最佳匹配时将会报错。



### 1.4.3、方法的重写——运行时多态

#### 1.4.3.1 方法重写的要求

1. 子类重写的方法`必须`和父类被重写的方法具有相同的`方法名称`、`参数列表`。

2. 子类重写的方法的返回值类型 `不能大于` 父类被重写的方法的返回值类型（即子类返回值的类型需要与父类相同或者返回父类的子类型）

   > 注意：如果返回值类型是**基本数据类型**和**void**，那么必须是相同

3. 子类重写的方法使用的访问权限 `不能小于` 父类被重写的方法的访问权限

   > 注意：子类不可见的方法不能重写

4. 子类方法抛出的异常 `不能大于` 父类被重写方法的异常



**此外，子类与父类中同名同参数的方法必须同时声明为非static的（重写），或者同时声明为static的（不属于重写）**。因为static方法是属于类的，子类无法覆盖父类的方法。

```java
class Parent {
    static void staticMethod() {
        System.out.println("Parent static method");
    }
    void instanceMethod() {
        System.out.println("Parent instance method");
    }
}

class Child extends Parent {
    // 静态方法不能覆盖，只是隐藏
    static void staticMethod() {
        System.out.println("Child static method");
    }
    @Override
    void instanceMethod() {
        System.out.println("Child instance method");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p = new Parent();
        Parent pc = new Child();
        Child c = new Child();

        // 调用静态方法
        p.staticMethod();  // 输出：Parent static method
        pc.staticMethod(); // 输出：Parent static method
        c.staticMethod();  // 输出：Child static method

        // 调用实例方法
        p.instanceMethod();  // 输出：Parent instance method
        pc.instanceMethod(); // 输出：Child instance method
        c.instanceMethod();  // 输出：Child instance method
    }
}
```



# =====

# 2、面向对象进阶

## 2.1 static关键字

### 2.1.1 static的认识

- 使用范围：
  - 在Java类中，可用static修饰属性、方法、代码块、内部类
- 被修饰后的成员具备以下特点：
  - 随着类的加载而加载
  - 优先于对象存在
  - 修饰的成员，被所有对象所共享
  - 访问权限允许时，可不创建对象，直接被类调用

### 2.1.2 静态变量

**静态变量的特点**

- 所有对象共享。
- 静态变量在本类中，可以在任意方法、代码块、构造器中直接使用。
- 在其他类中可以通过 “`类名.静态变量`” 或 “`对象.静态变量`” 直接访问
- 静态变量的get/set方法也静态的，当局部变量与静态变量`重名时`，使用“`类名.静态变量`”进行区分。

对应的内存结构：（以经典的JDK6内存解析为例，此时静态变量存储在方法区）

<img src="http://jason243.online/javase_songhongkang_images1/images/image-20220514183814514.png" alt="image-20220514183814514" style="zoom:67%;" />

> JDK8 在堆区，因为方法区（元空间）很难触发GC，无法及时清理，所以JDK8把字符串常量池和静态变量都移动到了堆区，也就是说从 JDK8 开始可以说java的所有对象都在堆区中。

### 2.1.3 静态方法

**静态方法的特点**

- 静态方法在本类的任意方法、代码块、构造器中都可以直接被调用。
- 静态方法在其他类中可以通过 `“类名.静态方法“` 或 `”对象.静态方法“` 的方式调用。
- 在static方法内部只能访问类的static修饰的属性或方法，不能访问类的非static的结构。
- 静态方法可以被子类继承，但不能被子类重写（不能Override，但是可以写自己的同名静态方法）。
- 静态方法的调用都只看编译时类型。
- 因为不需要实例就可以访问static方法，因此static方法内部不能有this，也不能有super。如果有重名问题，使用“类名.”进行区别。

```java
public class Son extends Father{
//    @Override //尝试重写静态方法，加上@Override编译报错，去掉Override不报错，但是也不是重写
    public static void fun(){
        System.out.println("Son.fun");
    }
}
```

### 2.1.4 笔试题：如下程序执行会不会报错

```java
public class StaticTest {
    public static void main(String[] args) {
        Demo test = null;
        test.hello();
    }
}

class Demo{
    public static void hello(){
        System.out.println("hello!");
    }
}
```

不报错。调用静态方法不需要对象实例。



## 2.2 理解main方法的语法

### 2.2.1 认识mian方法

- 由于JVM需要调用类的main()方法，所以该方法的访问权限必须是public
- 又因为JVM在执行main()方法时不必创建对象，所以该方法必须是static的
- 该方法接收一个String类型的数组参数，数组中保存执行Java命令时传递给所运行的类的参数。 
- 因为main() 方法是静态的，我们不能直接访问该类中的非静态成员，必须创建该类的一个实例对象后，才能通过这个对象去访问类中的非静态成员



### 2.2.2 笔试题：java文件名与缺省范围的类名不同是否可以编译运行

下面的程序是否可以正常编译、运行？

```java
//此处，Something类的文件名叫OtherThing.java
class Something {  // 注意这个类的修饰范围是缺省的不是 public，这是问题的关键所在
    public static void main(String[] something_to_do) {        
        System.out.println("Do something ...");
    }
}
```

可以运行，测试版本：JDK7 与 JDK11

- **因为class前面没有public，所以不会报错**
  - 编译之前的文件为OtherThing.java
  - 编译之后的文件为Something.class，没有OtherThing相关的文件，可以运行Something.class，java会正常执行其main方法。

- 额外细节补充：java本身支持对在同一个java文件中的与java文件名不同的非public类的编译
  - 一个Java文件里面只能有一个public类并且必须与文件名相同
  - 可以有多个缺省的class类，可以取别的名字，javac编译的时候会以类为单位进行编译，java文件中有多少个类就会生成多少个类的字节码，每个.class字节码都会以对应类的名字命名



## 2.3 代码块（类的成员之四）

- 代码块(或初始化块)的`作用`：

  - 对Java类或对象进行初始化

- 代码块(或初始化块)的`分类`：

  - 使用static修饰，称为静态代码块(static block)

  - 没有使用static修饰的，为非静态代码块。

    > 代码块只能使用static修饰或者缺省

- 类的成员有：构造器、成员变量、成员方法、代码块等

### 2.3.1 静态代码块

如果想要为静态变量初始化，可以直接在静态变量的声明后面直接赋值，也可以使用静态代码块。

#### 2.3.1.1 语法格式

在代码块的前面加static，就是静态代码块。

```java
【修饰符】 class 类{
	static{
        静态代码块
    }
}
```

#### 2.3.1.2 静态代码块的特点

- 可以有输出语句。
- 静态代码块的执行要先于非静态代码块。
  - 可以对类的属性、类的声明进行初始化操作。
  - 不可以对非静态的属性初始化（非静态的都没有加载进来）
- 静态代码块随着类的加载而加载，且只执行一次。
- 若有多个静态的代码块，那么按照从上到下的顺序依次执行。

### 2.3.2 非静态代码块

使用非静态代码块可以减少冗余代码

#### 2.3.2.1 语法格式

```java
【修饰符】 class 类{
    {
        非静态代码块
    }
    【修饰符】 构造器名(){
    	// 实例初始化代码
    }
    【修饰符】 构造器名(参数列表){
        // 实例初始化代码
    }
}
```

#### 2.3.2.4 非静态代码块的执行特点

- 可以有输出语句。
- 可以对类的属性、类的声明进行初始化操作。
- 可以调用**静态**的变量或方法。
- 若有多个非静态的代码块，那么按照从上到下的顺序依次执行。
- 每次创建对象的时候，都会执行一次。且先于构造器执行。

### 2.3.4 小结：实例变量赋值顺序

<img src="http://jason243.online/javase_songhongkang_images1/images/image-20220325230208941.png" alt="image-20220325230208941" style="zoom:50%;" />

### 2.3.5 辨析与总结（面试题）

练习1：分析加载顺序

```java
class Root{
	static{
		System.out.println("Root的静态初始化块1");	// 1
	}
	{
		System.out.println("Root的普通初始化块2");	// 2
	}
	public Root(){
		System.out.println("Root的无参数的构造器3");	// 3
	}
}
class Mid extends Root{
	static{
		System.out.println("Mid的静态初始化块4");	// 4 
	}
	{
		System.out.println("Mid的普通初始化块5");	// 5
	}
	public Mid(){
		System.out.println("Mid的无参数的构造器6");	// 6
	}
	public Mid(String msg){
		//通过this调用同一类中重载的构造器
		this();
		System.out.println("Mid的带参数构造器7，其参数值："
			+ msg);								// 7
	}
}
class Leaf extends Mid{
	static{
		System.out.println("Leaf的静态初始化块8");	// 8 
	}
	{
		System.out.println("Leaf的普通初始化块9");	// 9
	}	
	public Leaf(){
		//通过super调用父类中有一个字符串参数的构造器
		super("尚硅谷");
		System.out.println("Leaf的构造器10");	// 10
	}
}
public class LeafTest{
	public static void main(String[] args){
		new Leaf(); 
		//new Leaf();
	}
}
```

> 真实运行顺序 1、4、8、2、3、5、6、7、9、10
>
> 解开第二个new Leaf()注释，顺序：1、4、8、2、3、5、6、7、9、10、2、3、5、6、7、9、10

练习2：分析加载顺序

```java
class Father {
	static {
		System.out.println("11111111111");
	}
	{
		System.out.println("22222222222");
	}
	public Father() {
		System.out.println("33333333333");
	}
}

public class Son extends Father {
	static {
		System.out.println("44444444444");
	}
	{
		System.out.println("55555555555");
	}
	public Son() {
		System.out.println("66666666666");
	}
	public static void main(String[] args) { 
		System.out.println("77777777777");
		System.out.println("************************");
		new Son();
		System.out.println("************************");
		new Son();
		System.out.println("************************");
		new Father();
	}
}
```

> 运行顺序：
>
> 1、4、7
>
> 2、3、5、6、
>
> 2、3、5、6、
>
> 2、3



总结：

- JVM会先通过类加载器将类信息加载到元空间，类加载器会保证先加载父类再加载子类，所以调用子类时会优先加载父类，加载的时候会相应的执行类的**静态**代码块等东西。

  - 补充：

    - 上面所说的加载在JVM语境下指的是类加载器加载类的一整个完整过程。
    - 在加载类的时候会执行clinit方法对类进行初始化，clinit会自动收集静态变量、静态代码块等等进行执行和初始化，这个执行顺序是按照代码的编写顺序执行的。所以对应的执行顺序就是先执行父类的clinit再执行子类的clinit

    > 需要指出的是，JVM的类加载过程分为“加载阶段”、“链接阶段”、“初始化阶段”，这里的clinit是在初始化阶段执行，他会执行类中的静态代码块、为静态变量初始化（如果有赋值语句的话），而将类加载进内存是在加载阶段完成的，链接阶段又可以分为“验证、准备和解析”，其中准备阶段是给类的变量等分配内存，此时会对类变量赋默认值（比如int赋0），对final常量执行显示初始化即直接分配内存并赋好值，而解析阶段完成的事情是把符号引用变成直接引用

- 类加载完之后，如果new了类的对象，也会保证先new父类对象再new子类对象

  > new的时候会执行相应的非静态代码块、构造方法、为成员变量赋值，执行顺序按照代码顺序进行，构造方法就是JVM视角下的init方法

- 如果没有new对象而是直接调用子类的static方法，则不会new父类的对象，也不会执行父类和子类的构造函数、非静态代码块

  > 在JVM语境下，他们属于被动调用，所以不会执行类的初始化



## 2.4 final关键字

### 2.4.1 final的意义

final：最终的，不可更改的

### 2.4.2 final的使用

- final修饰类
- final修饰方法
- final修饰变量



## 2.5 单例(Singleton)设计模式

### 2.5.1 认识单例

- 所谓类的单例设计模式，就是采取一定的方法保证在整个的软件系统中，对某个类**只能存在一个对象实例**，并且该类只提供一个取得其对象实例的方法。

- **优点**：减少性能开销

### 2.5.2 实现思路

- 将 `类的构造器的访问权限设置为private`
- 在类的外部 `只能调用该类的某个静态方法` 以返回类内部创建的对象

### 2.5.3 单例模式的两种实现方式

#### 2.5.3.1 饿汉式

> 类初始化的时候同步构造一个类的对象

```java
class Singleton {
    // private
    private Singleton() {
    }
    // 创建类的静态对象
    private static Singleton single = new Singleton();
    // 提供公共的静态的方法，返回当前类的对象
    public static Singleton getInstance() {
        return single;
    }
}
```

#### 2.5.3.2 懒汉式

> 类的 `对象获取方法` 被调用的时候再创建类的对象

```java
class Singleton {
	// private
    private Singleton() {
    }
    // 先不创建对象
    private static Singleton single;
    // 提供公共的静态的方法，返回当前类的对象
    public static Singleton getInstance() {
        if(single == null) {
            single = new Singleton();
        }
        return single;
    }
}
```

#### 2.5.3.3 饿汉式 vs 懒汉式

饿汉式：

- 特点：`立即加载`，即在使用类的时候已经将对象创建完毕。
- 优点：**没有多线程安全问题**。
- 缺点：在某些特定条件下会`耗费内存`。

懒汉式：

- 特点：`延迟加载`，即在调用静态方法时实例才被创建。
- 优点：在某些特定条件下会`节约内存`。
- 缺点：`线程不安全`，根本不能保证单例的唯一性。
  - 说明：在多线程章节，会将懒汉式改造成线程安全的模式。

### 2.5.4 单例模式的优点及应用场景

当一个对象的产生需要比较多的资源时，如读取配置、产生其他依赖对象时，可以通过在应用启动时直接产生一个单例对象，然后永久驻留内存的方式来解决。

**应用场景**

- Windows的Task Manager (任务管理器)就是很典型的单例模式

- Windows的Recycle Bin (回收站)也是典型的单例应用

- Application 也是单例的典型应用

- 应用程序的日志应用，一般都使用单例模式实现，这一般是由于共享的日志文件一直处于打开状态，因为只

  能有一个实例去操作，否则内容不好追加。

- 数据库连接池的设计一般也是采用单例模式，因为数据库连接是一种数据库资源。



## 2.6 abstract关键字(抽象类与抽象方法)

### 2.6.1 语法格式

- **抽象类**：被abstract修饰的类。
- **抽象方法**：被abstract修饰没有方法体的方法。

> 注意：抽象方法没有方法体
>
> 子类对父类抽象方法的完成实现，我们将这种方法重写的操作，也叫做**实现方法**。

### 2.6.2 使用说明

1. 抽象类**不能创建对象**
2. 抽象类中，也有构造方法，是供子类创建对象时，初始化父类成员变量使用的。
3. 抽象类中，不一定包含抽象方法
4. 抽象类的子类，必须重写抽象父类中**所有的**抽象方法，除非该子类也是抽象类。 

### 2.6.3 注意事项

- 不能用abstract修饰变量、代码块、构造器；
- 不能用abstract修饰私有方法、静态方法、final的方法、final的类。

### 2.6.4 模板方法设计模式(TemplateMethod)

抽象类体现的就是一种模板模式的设计，抽象类作为多个子类的通用模板，子类在抽象类的基础上进行扩展、改造，但子类总体上会保留抽象类的行为方式。

**解决的问题**：

- 当功能内部一部分实现是确定的，另一部分实现是不确定的。这时可以把不确定的部分暴露出去，让子类去实现。
- 换句话说，在软件开发中实现一个算法时，整体步骤很固定、通用，这些步骤已经在父类中写好了。但是某些部分易变，易变部分可以抽象出来，供不同子类实现。这就是一种模板模式。

```java
abstract class Template {
    public final void getTime() {
        long start = System.currentTimeMillis();
        code();
        long end = System.currentTimeMillis();
        System.out.println("执行时间是：" + (end - start));
    }

    public abstract void code();
}

class SubTemplate extends Template {
    public void code() {
        for (int i = 0; i < 10000; i++) {
            System.out.println(i);
        }
    }
}

```

模板方法设计模式是编程中经常用得到的模式。各个框架、类库中都有他的影子，比如常见的有：

- 数据库访问的封装
- Junit单元测试
- JavaWeb的Servlet中关于doGet/doPost方法调用
- Hibernate中模板程序
- Spring中JDBCTemlate、HibernateTemplate等

### 2.6.5 思考与练习

**思考：**

- 问题1：为什么抽象类不可以使用final关键字声明？

  看完上面的内容很显然。

- 问题2：一个抽象类中可以定义构造器吗？

  可以，上面明说了。

- 问题3：是否可以这样理解：抽象类就是比普通类多定义了抽象方法，除了不能直接进行类的实例化操作之外，并没有任何的不同？

  不完全正确。**核心区别**：

  | **特性**     | **抽象类**             | **普通类**         |
  | ------------ | ---------------------- | ------------------ |
  | **抽象方法** | 可以包含抽象方法       | 不能包含抽象方法   |
  | **实例化**   | 不能直接实例化         | 可以直接实例化     |
  | **继承要求** | 必须被继承才能使用     | 无需被继承即可使用 |
  | **设计目的** | 作为模板，定义部分实现 | 作为完整的功能单元 |



## 2.7 接口(interface)

### 2.7.2 概述

接口就是规范，定义的是一组规则，体现了现实世界中“如果你是/要...则必须能...”的思想。继承是一个"是不是"的is-a关系，而接口实现则是 "能不能"的`has-a`关系。

> 接口的本质是契约、标准、规范，就像我们的法律一样。制定好后大家都要遵守。

### 2.7.3 定义格式

接口的定义，它与定义类方式相似，但是使用 `interface` 关键字。它也会被编译成.class文件，但一定要明确它并不是类，而是另外一种引用数据类型。

> 引用数据类型：数组，类，枚举，接口，注解。

#### 2.7.3.1 接口的声明格式

```java
[修饰符] interface 接口名{
    //接口的成员列表：
    // 公共的静态常量
    // 公共的抽象方法
    
    // 公共的默认方法（JDK1.8以上）
    // 公共的静态方法（JDK1.8以上）
    // 私有方法（JDK1.9以上）
}
```

#### 2.7.3.2 接口的成员说明

**在JDK8.0 之前**，接口中只允许出现：

（1）公共的静态的常量：其中`public static final`可以省略

（2）公共的抽象的方法：其中`public abstract`可以省略

> 理解：接口是从多个相似类中抽象出来的规范，不需要提供具体实现

**在JDK8.0 时**，接口中允许声明`默认方法`和`静态方法`：

（3）公共的默认的方法：其中public 可以省略，建议保留，但是default不能省略

（4）公共的静态的方法：其中public 可以省略，建议保留，但是static不能省略

**在JDK9.0 时**，接口又增加了：

（5）私有方法

除此之外，接口中没有构造器，没有初始化块，因为接口中没有成员变量需要动态初始化。

### 2.7.4 接口的使用规则

**1、类实现接口（implements）**

接口**不能创建对象**，但是可以被类实现（`implements` ，类似于被继承）。

**注意：**

1. 如果接口的实现类是非抽象类，那么必须`重写接口中所有抽象方法`。

2. 默认方法可以选择保留，也可以重写。

   > 重写时，default单词就不要再写了，它只用于在接口中表示默认方法，到类中就没有默认方法的概念了

3. 接口中的静态方法不能被继承也不能被重写

**2、接口的多实现（implements）**

一个类可以实现多个接口的，这叫做接口的`多实现`。并且，一个类能继承一个父类，同时实现多个接口。

> 接口中，有多个抽象方法时，实现类必须重写所有抽象方法。**如果抽象方法有重名的，只需要重写一次**。

**3、接口的多继承(extends)**

一个接口能继承另一个或者多个接口，接口的继承也使用 `extends` 关键字，子接口继承父接口的方法。

> 所有父接口的抽象方法都有重写。
>
> 方法签名相同的抽象方法只需要实现一次。

**4、接口与实现类对象构成多态引用**

接口类型的变量与实现类的对象之间，也可以构成多态引用。通过接口类型的变量调用方法，最终执行的是你new的实现类对象实现的方法体。

> 类似 用父类对象接收子类的引用

**5、使用接口的静态成员**

接口不能直接创建对象，但是可以通过接口名直接调用接口的静态方法和静态常量。

**6、使用接口的非静态方法**

- 对于接口的静态方法，直接且只能使用“`接口名.`”进行调用即可
- 对于接口的抽象方法、默认方法，只能通过实现类对象才可以调用

### 2.7.5 JDK8中相关冲突问题

#### 2.7.5.1 默认方法冲突问题

**（1）类优先原则**

当一个类，既继承一个父类，又实现若干个接口时，父类中的成员方法与接口中的抽象方法重名，子类就近选择执行父类的成员方法。代码如下：

定义接口：

```java
package com.atguigu.interfacetype;

public interface Friend {
    default void date(){//约会
        System.out.println("吃喝玩乐");
    }
}
```

定义父类：

```java
package com.atguigu.interfacetype;

public class Father {
    public void date(){//约会
        System.out.println("爸爸约吃饭");
    }
}
```

定义子类：

```java
package com.atguigu.interfacetype;

public class Son extends Father implements Friend {
    @Override
    public void date() {
        //(1)不重写默认保留父类的
        //(2)调用父类被重写的
//        super.date();
        //(3)保留父接口的
//        Friend.super.date();
        //(4)完全重写
        System.out.println("跟康师傅学Java");
    }
}
```

**（2）接口冲突（左右为难）**

- 当一个类同时实现了多个父接口，而多个父接口中包含方法签名相同的默认方法时，怎么办呢？

![](http://jason243.online/javase_songhongkang_images1/images/选择困难.jpg)

无论你多难抉择，最终都是要做出选择的。

声明接口：

```java
package com.atguigu.interfacetype;

public interface BoyFriend {
    default void date(){//约会
        System.out.println("神秘约会");
    }
}
```

选择保留其中一个，通过“`接口名.super.方法名`"的方法选择保留哪个接口的默认方法。

```java
package com.atguigu.interfacetype;

public class Girl implements Friend,BoyFriend{

    @Override
    public void date() {
        //(1)保留其中一个父接口的
//        Friend.super.date();
//        BoyFriend.super.date();
        //(2)完全重写
        System.out.println("跟康师傅学Java");
    }

}
```

- 当一个子接口同时继承了多个接口，而多个父接口中包含方法签名相同的默认方法时，怎么办呢？

  - **子接口必须覆盖冲突的默认方法**：
    如果多个父接口中存在**相同方法签名**的默认方法，子接口必须重新定义该方法，否则会编译报错。

  - **三种覆盖方式**：

    - **方式一**：子接口提供自己的默认方法实现。
    - **方式二**：子接口将方法改为抽象方法（不提供实现，交由实现类处理）。
    - **方式三**：通过`InterfaceName.super.methodName()`指定调用某个父接口的默认方法。

    > 小贴士：
    >
    > 子接口重写默认方法时，default关键字可以保留。
    >
    > 子类重写默认方法时，default关键字不可以保留。

多接口继承的总结

| 成员类型     | 冲突情况 | 冲突解决                                                     |
| ------------ | -------- | ------------------------------------------------------------ |
| **静态变量** | 无冲突   | 必须通过接口名访问（如 `USB2.MAX_SPEED`），不会有歧义。      |
| **静态方法** | 无冲突   | 必须通过接口名访问（如 `USB2.show()`），不会有歧义。         |
| **抽象方法** | 无冲突   | 子类或实现类只需实现一次即可。                               |
| **默认方法** | 有冲突   | 子类或子接口必须显式解决冲突（重写方法或显式调用某父接口的方法）。 |

#### 2.7.5.2 常量冲突问题

常量冲突的存在情况：

- 当子类继承父类又实现父接口，而父类中存在与父接口常量同名的成员变量，并且该成员变量名在子类中仍然可见。
- 当子类同时实现多个接口，而多个接口存在相同同名常量。

此时在子类中想要引用父类或父接口的同名的常量或成员变量时，就会有冲突问题。

**此时实现类中必须显式的知名使用的是哪里的常量/变量**

父类和父接口：

```java
package com.atguigu.interfacetype;

public class SuperClass {
    int x = 1;
}
```

```java
package com.atguigu.interfacetype;

public interface SuperInterface {
    int x = 2;
    int y = 2;
}
```

```java
package com.atguigu.interfacetype;

public interface MotherInterface {
    int x = 3;
}
```

子类：

```java
package com.atguigu.interfacetype;

public class SubClass extends SuperClass implements SuperInterface,MotherInterface {
    public void method(){
//        System.out.println("x = " + x);//模糊不清
        System.out.println("super.x = " + super.x);
        System.out.println("SuperInterface.x = " + SuperInterface.x);
        System.out.println("MotherInterface.x = " + MotherInterface.x);
        System.out.println("y = " + y);//没有重名问题，可以直接访问
    }
}
```

### 2.7.6 接口的总结与面试题

- 接口本身不能创建对象，只能创建接口的实现类对象，接口类型的变量可以与实现类对象构成多态引用。
- 声明接口用interface，接口的成员声明有限制：
  - （1）公共的静态常量
  - （2）公共的抽象方法
  - （3）公共的默认方法（JDK8.0 及以上）
  - （4）公共的静态方法（JDK8.0 及以上）
  - （5）私有方法（JDK9.0 及以上）
- 类可以实现接口，关键字是implements，而且支持多实现。如果实现类不是抽象类，就必须实现接口中所有的抽象方法。如果实现类既要继承父类又要实现父接口，那么继承（extends）在前，实现（implements）在后。
- 接口可以继承接口，关键字是extends，而且支持多继承。
- 接口的默认方法可以选择重写或不重写。如果有冲突问题，另行处理。子类重写父接口的默认方法，要去掉default，子接口重写父接口的默认方法，不要去掉default。
- 接口的静态方法不能被继承，也不能被重写。接口的静态方法只能通过“接口名.静态方法名”进行调用。

**面试题**

**1、为什么接口中只能声明公共的静态的常量？**

因为接口是标准规范，那么在规范中需要声明一些底线边界值，当实现者在实现这些规范时，不能去随意修改和触碰这些底线，否则就有“危险”。

例如：USB1.0规范中规定最大传输速率是1.5Mbps，最大输出电流是5V/500mA

​           USB3.0规范中规定最大传输速率是5Gbps(500MB/s)，最大输出电流是5V/900mA

例如：尚硅谷学生行为规范中规定学员，早上8:25之前进班，晚上21:30之后离开等等。

**2、为什么JDK8.0 之后允许接口定义静态方法和默认方法呢？**

**因为不允许的话违反了接口作为一个抽象标准定义的概念。**

- `静态方法`：因为之前的标准类库设计中，有很多Collection/Colletions或者Path/Paths这样成对的接口和类，后面的类中都是静态方法，而这些静态方法都是为前面的接口服务的，那么这样设计一对API，不如把静态方法直接定义到接口中使用和维护更方便。

- `默认方法`：
  - （1）我们要在已有的老版接口中提供新方法时，如果添加抽象方法，就会涉及到原来使用这些接口的类就会有问题，那么为了保持与旧版本代码的兼容性，只能允许在接口中定义默认方法实现。比如：Java8中对Collection、List、Comparator等接口提供了丰富的默认方法。
  - （2）当我们接口的某个抽象方法，在很多实现类中的实现代码是一样的，此时将这个抽象方法设计为默认方法更为合适，那么实现类就可以选择重写，也可以选择不重写。

**3、为什么JDK1.9要允许接口定义私有方法呢？因为我们说接口是规范，规范是需要公开让大家遵守的。**

**私有方法**：因为有了默认方法和静态方法这样具有具体实现的方法，那么就可能出现多个方法由共同的代码可以抽取，而这些共同的代码抽取出来的方法又只希望在接口内部使用，所以就增加了私有方法。

### 2.7.7 接口与抽象类之间的对比

![image-20220328002053452](http://jason243.online/javase_songhongkang_images1/images/image-20220328002053452.png)

> 在开发中，常看到一个类不是去继承一个已经实现好的类，而是要么继承抽象类，要么实现接口。

### 2.7.8 面试题

**笔试题：**排错

```java
interface Playable {
    void play();
}

interface Bounceable {
    void play();
}

interface Rollable extends Playable, Bounceable {
    Ball ball = new Ball("PingPang");
}

class Ball implements Rollable {
    private String name;

    public String getName() {
        return name;
    }

    public Ball(String name) {
        this.name = name;
    }

    public void play() {
        ball = new Ball("Football");	// 不能修改常量，这里有问题
        System.out.println(ball.getName());	// 注意这里打印的是ball的name，也就是PingPang
//        System.out.println(this.getName()); // 这样可以打印当前实例化对象的name
    }
}
```



## 2.8 8. 内部类（InnerClass)

### 8.1 概述

- 将一个类A定义在另一个类B里面，里面的那个类A就称为`内部类（InnerClass）`，类B则称为`外部类（OuterClass）`。

- 使用内部类是为了遵循`高内聚、低耦合`的面向对象开发原则。

- 根据内部类声明的位置（如同变量的分类），我们可以分为：

![image-20221124223912529](http://jason243.online/javase_songhongkang_images1/images/image-20221124223912529.png)

### 8.2 成员内部类

#### 8.2.1 概述

**语法格式：**

```java
[修饰符] class 外部类{
    [其他修饰符] [static] class 内部类{
    }
}
```

**成员内部类的使用特征，概括来讲有如下两种角色：**

- 成员内部类作为`类的成员的角色`：
  - 和外部类不同，Inner class还可以声明为private或protected；
  - 可以调用外部类的结构
  - Inner class 可以声明为static的，但此时就不能再使用外层类的非static的成员变量
- 成员内部类作为`类的角色`：
  - 可以在内部定义属性、方法、构造器等结构
  - 可以继承自己的想要继承的父类，实现自己想要实现的父接口们，和外部类的父类和父接口无关
  - 可以声明为abstract类 ，因此可以被其它的内部类继承
  - 可以声明为final的，表示不能被继承
  - 编译以后生成OuterClass$InnerClass.class字节码文件（也适用于局部内部类）

注意点：

1. 外部类访问成员内部类的成员，需要“内部类.成员”或“内部类对象.成员”的方式
2. 成员内部类可以直接使用外部类的所有成员，包括私有的数据
3. 当想要在外部类的静态成员部分使用内部类时，可以考虑内部类声明为静态的

#### 8.2.2 创建成员内部类对象

- 实例化静态内部类

```
外部类名.静态内部类名 变量 = 外部类名.静态内部类名();
变量.非静态方法();
```

- 实例化非静态内部类

```
外部类名 变量1 = new 外部类();
外部类名.非静态内部类名 变量2 = 变量1.new 非静态内部类名();
变量2.非静态方法();
```

### 8.3 局部内部类

#### 8.3.1 非匿名局部内部类

语法格式：

```java
[修饰符] class 外部类{
    [修饰符] 返回值类型  方法名(形参列表){
            [final/abstract] class 内部类{
    	}
    }    
}
```

- 编译后有自己的独立的字节码文件，只不过在内部类名前面冠以外部类名、$符号、编号。
  - 这里有编号是因为同一个外部类中，不同的方法中存在相同名称的局部内部类

- 和成员内部类不同的是，它前面不能有权限修饰符等
- 局部内部类如同局部变量一样，有作用域
- 局部内部类中是否能访问外部类的非静态的成员，取决于所在的方法

#### 8.3.2 匿名内部类

因为考虑到这个子类或实现类是一次性的，那么我们“费尽心机”的给它取名字，就显得多余。那么我们完全可以使用匿名内部类的方式来实现，避免给类命名的问题。

```java
new 父类([实参列表]){
    重写方法...
}
```

```java
new 父接口(){
    重写方法...
}
```

举例1：使用匿名内部类的对象直接调用方法：

```java
interface A{
	void a();
}
public class Test{
    public static void main(String[] args){
    	new A(){
			@Override
			public void a() {
				System.out.println("aaaa");
			}
    	}.a();
    }
}
```

举例2：通过父类或父接口的变量多态引用匿名内部类的对象

```java
interface A{
	void a();
}
public class Test{
    public static void main(String[] args){
    	A obj = new A(){
			@Override
			public void a() {
				System.out.println("aaaa");
			}
    	};
    	obj.a();
    }
}
```

举例3：匿名内部类的对象作为实参

```java
interface A{
	void method();
}
public class Test{
    public static void test(A a){
    	a.method();
    }
    
    public static void main(String[] args){
    	test(new A(){

			@Override
			public void method() {
				System.out.println("aaaa");
			}
    	});
    }   
}
```



## 2.9 枚举类

### 2.9.1 概述

- 枚举类型本质上也是一种类，只不过是这个类的对象是有限的、固定的几个，不能让用户随意创建。
- **若枚举只有一个对象, 则可以作为一种单例模式的实现方式。**
- 枚举类的实现：
  - 在JDK5.0 之前，需要程序员自定义枚举类型。
  - 在JDK5.0 之后，Java支持`enum`关键字来快速定义枚举类型。

### 2.9.2 定义枚举类（JDK5.0 之后）

#### 2.9.2.1 enum关键字声明枚举

```java
【修饰符】 enum 枚举类名{
    常量对象列表
}

【修饰符】 enum 枚举类名{
    常量对象列表;
    
    对象的实例变量列表;
}
```

举例1：

```java
package com.atguigu.enumeration;

public enum Week {
    MONDAY,TUESDAY,WEDNESDAY,THURSDAY,FRIDAY,SATURDAY,SUNDAY;
}
```

```java
public class TestEnum {
	public static void main(String[] args) {
		Season spring = Season.SPRING;
		System.out.println(spring);
	}
}
```

#### 2.9.2.2 enum方式定义的要求和特点

- 枚举类的常量对象列表必须在枚举类的首行，因为是常量，所以建议大写。
- 列出的实例系统会自动添加 public static final 修饰。
- 如果常量对象列表后面没有其他代码，那么“；”可以省略，否则不可以省略“；”。
- 编译器给枚举类默认提供的是private的无参构造，如果枚举类需要的是无参构造，就不需要声明，写常量对象列表时也不用加参数
- 如果枚举类需要的是有参构造，需要手动定义，有参构造的private可以省略，调用有参构造的方法就是在常量对象名后面加(实参列表)就可以。
- 枚举类默认继承的是java.lang.Enum类，因此不能再继承其他的类型。
- JDK5.0 之后switch，提供支持枚举类型，case后面可以写枚举常量名，无需添加枚举类作为限定。

举例2：

```java
public enum SeasonEnum {
    SPRING("春天","春风又绿江南岸"),
    SUMMER("夏天","映日荷花别样红"),
    AUTUMN("秋天","秋水共长天一色"),
    WINTER("冬天","窗含西岭千秋雪");

    private final String seasonName;
    private final String seasonDesc;
    
    private SeasonEnum(String seasonName, String seasonDesc) {
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }
    public String getSeasonName() {
        return seasonName;
    }
    public String getSeasonDesc() {
        return seasonDesc;
    }
}
```

> 经验之谈：
>
> 开发中，当需要定义一组常量时，强烈建议使用枚举类。

### 2.9.3 enum中常用方法

- String toString(): 默认返回的是常量名（对象名），可以继续手动重写该方法！
-  static 枚举类型[] values():返回枚举类型的对象数组。该方法可以很方便地遍历所有的枚举值，是一个静态方法
- static 枚举类型 valueOf(String name)：可以把一个字符串转为对应的枚举类对象。要求字符串必须是枚举类对象的“名字”。如不是，会有运行时异常：IllegalArgumentException。
- String name():得到当前枚举常量的名称。建议优先使用toString()。
- int ordinal():返回当前枚举常量的次序号，默认从0开始

### 2.9.4 实现接口的枚举类

- 和普通 Java 类一样，枚举类可以实现一个或多个接口
- 若每个枚举值在调用实现的接口方法呈现相同的行为方式，则只要统一实现该方法即可。
- 若需要每个枚举值在调用实现的接口方法呈现出不同的行为方式，则可以让每个枚举值分别来实现该方法

语法：

```java
//1、枚举类可以像普通的类一样，实现接口，并且可以多个，但要求必须实现里面所有的抽象方法！
enum A implements 接口1，接口2{
	//抽象方法的实现
}

//2、如果枚举类的常量可以继续重写抽象方法!
enum A implements 接口1，接口2{
    常量名1(参数){
        //抽象方法的实现或重写
    },
    常量名2(参数){
        //抽象方法的实现或重写
    },
    //...
}
```

举例：

```java
interface Info{
	void show();
}

//使用enum关键字定义枚举类
enum Season1 implements Info{
	//1. 创建枚举类中的对象,声明在enum枚举类的首位
	SPRING("春天","春暖花开"){
        // 可以加一个 @Override
		public void show(){
			System.out.println("春天在哪里？");
		}
	},
	SUMMER("夏天","夏日炎炎"){
		public void show(){
			System.out.println("宁静的夏天");
		}
	},
	AUTUMN("秋天","秋高气爽"){
		public void show(){
			System.out.println("秋天是用来分手的季节");
		}
	},
	WINTER("冬天","白雪皑皑"){
		public void show(){
			System.out.println("2002年的第一场雪");
		}
	};
	
	//2. 声明每个对象拥有的属性:private final修饰
	private final String SEASON_NAME;
	private final String SEASON_DESC;
	
	//3. 私有化类的构造器
	private Season1(String seasonName,String seasonDesc){
		this.SEASON_NAME = seasonName;
		this.SEASON_DESC = seasonDesc;
	}
	
	public String getSEASON_NAME() {
		return SEASON_NAME;
	}

	public String getSEASON_DESC() {
		return SEASON_DESC;
	}
}
```



## 2.10 包装类

### 2.10.1 有哪些包装类

<img src="http://jason243.online/javase_songhongkang_images1/images/image-20220329001912486.png" alt="image-20220329001912486" style="zoom:80%;" />

### 2.10.2 自定义包装类

```java
public class MyInteger {
    int value;

    public MyInteger() {
    }

    public MyInteger(int value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return String.valueOf(value);
    }
}
```

### 2.10.3 包装类与基本数据类型间的转换

- **装箱：把基本数据类型转为包装类对象**

- **拆箱：把包装类对象拆为基本数据类型**

- **自动装箱与拆箱：**

### 2.10.4 基本数据类型、包装类与字符串间的转换

**（1）基本数据类型转为字符串**

**方式1：**调用字符串重载的valueOf()方法

```java
int a = 10;
//String str = a;//错误的

String str = String.valueOf(a);
```

**方式2：**更直接的方式

```java
int a = 10;

String str = a + "";
```

**（2）字符串转为基本数据类型**

**方式1：**除了Character类之外，其他所有包装类都具有parseXxx静态方法可以将字符串参数转换为对应的基本类型，例如：

- `public static int parseInt(String s)`：将字符串参数转换为对应的int基本类型。
- `public static long parseLong(String s)`：将字符串参数转换为对应的long基本类型。
- `public static double parseDouble(String s)`：将字符串参数转换为对应的double基本类型。

**方式2：**字符串转为包装类，然后可以自动拆箱为基本数据类型

- ```public static Integer valueOf(String s)```：将字符串参数转换为对应的Integer包装类，然后可以自动拆箱为int基本类型
- ```public static Long valueOf(String s)```：将字符串参数转换为对应的Long包装类，然后可以自动拆箱为long基本类型
- ```public static Double valueOf(String s)```：将字符串参数转换为对应的Double包装类，然后可以自动拆箱为double基本类型

注意:如果字符串参数的内容无法正确转换为对应的基本类型，则会抛出`java.lang.NumberFormatException`异常。

**方式3：**通过包装类的构造器实现

```java
int a = Integer.parseInt("整数的字符串");
double d = Double.parseDouble("小数的字符串");
boolean b = Boolean.parseBoolean("true或false");

int a = Integer.valueOf("整数的字符串");
double d = Double.valueOf("小数的字符串");
boolean b = Boolean.valueOf("true或false");

int i = new Integer(“12”);
```

### 2.10.5 包装类的其它API

#### 2.10.5.1 数据类型的最大最小值

```java
Integer.MAX_VALUE和Integer.MIN_VALUE
    
Long.MAX_VALUE和Long.MIN_VALUE
    
Double.MAX_VALUE和Double.MIN_VALUE
```

#### 2.10.5.2 字符转大小写

```java
Character.toUpperCase('x');

Character.toLowerCase('X');
```

#### 2.10.5.3 整数转进制

```java
Integer.toBinaryString(int i) 
    
Integer.toHexString(int i)
    
Integer.toOctalString(int i)
```

#### 2.10.5.4 比较的方法

```java
Double.compare(double d1, double d2)
    
Integer.compare(int x, int y) 
```

