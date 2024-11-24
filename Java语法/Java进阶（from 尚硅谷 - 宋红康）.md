# Java进阶

# 1、面向对象

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
     结合②，结论：在构造器的首行，"this(形参列表)" 和 "super(形参列表)"只能二选一。

④ 如果在子类构造器的首行既没有显示调用"this(形参列表)"，也没有显式调用"super(形参列表)"，则子类此构造器默认调用"super()"，即调用父类中空参的构造器。





## 1.2、封装（Encapsulation）

<img src="http://jason243.online/javase_songhongkang/Object/java001.png" style="zoom:67%;"/>



## 1.3、继承（Inheritance）

### 1.3.1 继承中的语法格式

通过 `extends` 关键字，可以声明一个类B继承另外一个类A，定义格式如下：

```java
[修饰符] class 类A {
	...
}

[修饰符] class 类B extends 类A {
	...
}

```



### 1.3.2 继承中的基本概念

类B，称为子类、派生类(derived class)、SubClass

类A，称为父类、超类、基类(base class)、SuperClass



### 1.3.3 继承的细节说明

**1、子类会继承父类所有的实例变量和实例方法**

- 当子类对象调用方法时，编译器会先在子类模板中看该类是否有这个方法，如果没找到，会看它的父类甚至父类的父类是否声明了这个方法，遵循`从下往上`找的顺序，找到了就停止，一直到根父类都没有找到，就会报编译错误。

所以继承意味着子类的对象除了看子类的类模板还要看父类的类模板。

**2、子类不能直接访问父类中私有的(private)的成员变量和方法**

子类虽会继承父类私有(private)的成员变量，但子类不能对继承的私有成员变量直接进行访问

**3、在Java 中，继承的关键字用的是“extends”，即子类不是父类的子集，而是对父类的“扩展”**

**4、Java支持多层继承(继承体系)**

<img src="http://jason243.online/javase_songhongkang/Object/java003.png" alt="image-20220323225441417" style="zoom:67%;" />

**5、一个父类可以同时拥有多个子类**

**6、Java只支持单继承，不支持多重继承**



## 1.4、多态（Polymorphism）

### 1.4.1、对象的多态性

多态性，是面向对象中最重要的概念

**对象的多态性：父类的引用指向子类的对象**

格式：（父类类型：指子类继承的父类类型，或者实现的接口类型）

```java
父类类型 变量名 = 子类对象；
```

举例：

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

**好处**：变量引用的子类对象不同，执行的方法就不同，实现动态绑定。代码编写更灵活、功能更强大，可维护性和扩展性更好了。

**弊端**：**一个引用类型变量如果声明为父类的类型，但实际引用的是子类对象，那么该变量就不能再访问子类中添加的属性和方法。**

```java
Student m = new Student();
m.school = "pku"; 	//合法,Student类有school成员变量
Person e = new Student(); 
e.school = "pku";	//非法,Person类没有school成员变量

// 属性是在编译时确定的，编译时e为Person类型，没有school成员变量，因而编译错误。
```



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



**向上转型（Upcasting）**

- **向上转型**是指将子类对象赋值给父类类型的变量。
- 这是安全的，Java 会自动完成。
- 转型后，**编译时只能调用父类中声明的方法**，但这些方法在运行时会动态绑定到子类的实现（虚方法机制）。

```java
// 向上转型：Student对象赋值给Person类型变量
Person person = new Student();
```



**向下转型（Downcasting）**

- **向下转型**是指将父类类型的变量强制转换为子类类型。
- 这种转型需要手动完成（强制类型转换）。
- 如果父类变量的实际运行时类型不是目标子类，会抛出 `ClassCastException`。

```java
// 向上转型
Person person = new Student();

// 向下转型
Student student = (Student) person;

// 调用子类特有的方法
student.study();

// 如果向下转型失败（运行时类型不匹配），会抛出ClassCastException
Person anotherPerson = new Person();
// Student anotherStudent = (Student) anotherPerson; // 运行时报错
```



### 1.4.2、方法的重载——编译时多态

#### 1.4.2.1 方法重载：

- 在同一个类中，允许存在一个以上的同名方法，只要它们的**参数列表不同**即可。
- **参数列表不同**，意味着参数个数或参数类型的不同。

#### 1.4.2.2 重载的特点：

- 与修饰符、返回值类型无关，**只看参数列表**，且参数列表必须不同（参数个数或参数类型）。
- 调用时，根据方法参数列表的不同来区别。

#### 1.4.2.3 重载方法调用：

- JVM 通过方法的参数列表，调用匹配的方法。
  1. **先找个数、类型匹配的**。
  2. **再找个数和类型可以兼容的**，如果没有完全匹配的方法，但有多个方法可以兼容，且 JVM 无法判断最佳匹配时将会报错。

```java
// 调用不明确（报错场景）
class Test {
    void print(double a) {
        System.out.println("double: " + a);
    }

    void print(Float a) {
        System.out.println("Float: " + a);
    }

    public static void main(String[] args) {
        Test t = new Test();
        t.print(5); // 报错：无法确定调用哪个方法（double 还是 Float）
    }
}
```



### 1.4.3、方法的重写——运行时多态

#### 1.4.3.1 方法重写的要求

1. 子类重写的方法`必须`和父类被重写的方法具有相同的`方法名称`、`参数列表`。
2. 子类重写的方法的返回值类型`不能大于`父类被重写的方法的返回值类型。（即子类返回值的类型需要与父类相同，对于返回值是非基本类型或void的情况，子类返回值还可以是父类返回值的子类型）。

```java
class Person {
    public Person getPerson() {
        return new Person();
    }
}

class Student extends Person {
    @Override
    public Student getPerson() { // Student 是 Person 的子类，合法
        return new Student();
    }
}
```

> 注意：如果返回值类型是**基本数据类型**和**void**，那么必须是相同

3. 子类重写的方法使用的访问权限`不能小于`父类被重写的方法的访问权限。（public > protected > 缺省 > private）

> 注意：① 父类私有方法不能重写   ② 跨包的父类缺省的方法也不能重写
>
> 即子类不可见的方法不能重写

4. 子类方法抛出的异常不能大于父类被重写方法的异常



**此外，子类与父类中同名同参数的方法必须同时声明为非static的(即为重写)，或者同时声明为static的（不是重写）**。因为static方法是属于类的，子类无法覆盖父类的方法。

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

- 静态方法：
  - 静态方法在编译时绑定，调用的是引用变量的类型所属类的方法，而非实际对象的类型的方法。
  - `pc.staticMethod()` 调用的是 `Parent` 的静态方法，而非 `Child` 的静态方法。
- 实例方法：
  - 实例方法是动态绑定，`pc.instanceMethod()` 会根据运行时实际对象类型调用 `Child` 的实现。



=====

# 2、泛型(Generic)

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

  List<Integer> list = new ArrayList<Integer>();

  List<Integer> list = new ArrayList<>(); //类型推断

- 泛型，也称为泛型参数，即参数的类型，只能使用引用数据类型进行赋值。（不能使用基本数据类型，可以使用包装类替换）

- 集合声明时，声明泛型参数。在使用集合时，可以具体指明泛型的类型。一旦指明，类或接口内部，凡是使用泛型参数的位置，都指定为具体的参数类型。如果没有指明的话，看做是Object类型。



## 3. 自定义泛型结构

### 3.1 泛型的基础说明

**1、<类型>这种语法形式就叫泛型。**

- <类型>的形式我们称为类型参数，这里的"类型"习惯上使用T表示，是Type的缩写。即：<T>。
- <T>：代表未知的数据类型，我们可以指定为<String>，<Integer>，<Circle>等。
  - 类比方法的参数的概念，我们把<T>，称为类型形参，将<Circle>称为类型实参，有助于我们理解泛型
- 这里的T，可以替换成K，V等任意字母。

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

   ```java
   Box<Integer> intBox = new Box<>(10); // 使用 Integer，而不是 int
   Box<Double> doubleBox = new Box<>(5.5); // 使用 Double，而不是 double
   ```

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

2. **JDK 7+ 支持泛型简化写法**  
   **示例**：

   ```java
   List<String> list = new ArrayList<>(); // 类型推断，省略右侧的 <String>
   list.add("Hello");
   
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

如果B是A的一个子类型（子类或者子接口），而G是具有泛型声明的类或接口，G<B>并不是G<A>的子类型！

比如：String是Object的子类，但是List<String>并不是List<Object>的子类。

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

当我们声明一个变量/形参时，这个变量/形参的类型是一个泛型类或泛型接口，例如：Comparator<T>类型，但是我们仍然无法确定这个泛型类或泛型接口的类型变量<T>的具体类型，此时我们考虑使用类型通配符 ? 。

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

  - 使用时指定的类型必须是继承某个类，或者实现某个接口，即<= 

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

- `? extends T` 表示泛型类型是 `T` **或 T 的子类**。
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

- `? super T` 表示泛型类型是 `T` **或 T 的父类**。
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





