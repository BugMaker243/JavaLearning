# Collections集合框架

## 1. 集合框架概述

### 1.2 数组的特点与弊端

- 数组在内存存储方面的`特点`：
  - 数组初始化以后，长度就确定了。
  - 数组中的添加的元素是依次紧密排列的，有序的，可以重复的。
  - 数组声明的类型，就决定了进行元素初始化时的类型。不是此类型的变量，就不能添加。
  - 可以存储基本数据类型值，也可以存储引用数据类型的变量
- 数组在存储数据方面的`弊端`：
  - 数组初始化以后，长度就不可变了，不便于扩展
  - 数组中提供的属性和方法少，不便于进行添加、删除、插入、获取元素个数等操作，且效率不高。
  - 数组存储数据的特点单一，只能存储有序的、可以重复的数据
- Java 集合框架中的类可以用于存储多个`对象`，还可用于保存具有`映射关系`的关联数组。

### 1.3 Java集合框架体系

Java 集合可分为 Collection 和 Map 两大体系：

- Collection接口：用于存储一个一个的数据，也称`单列数据集合`。
  - List子接口：用来存储有序的、可以重复的数据（主要用来替换数组，"动态"数组）
    - 实现类：ArrayList(主要实现类)、LinkedList、Vector
  - Set子接口：用来存储无序的、不可重复的数据（类似于高中讲的"集合"）
    - 实现类：HashSet(主要实现类)、LinkedHashSet、TreeSet
- Map接口：用于存储具有映射关系“key-value对”的集合，即一对一对的数据，也称`双列数据集合`。(类似于高中的函数、映射。(x1,y1),(x2,y2) ---> y = f(x) )
  - HashMap(主要实现类)、LinkedHashMap、TreeMap、Hashtable、Properties

## 2. Collection接口及方法

- JDK不提供此接口的任何直接实现，而是提供更具体的子接口（如：Set和List）去实现。
- Collection 接口是 List和Set接口的父接口

### 2.1 添加

（1）add(E obj)：添加元素对象到当前集合中
（2）addAll(Collection other)：添加other集合中的所有元素对象到当前集合中，即this = this ∪ other

> 注意：coll.addAll(other);与coll.add(other);
>
> ![](http://jason243.online/javase_songhongkang/images/1563548078274.png)

### 2.2 判断

（3）int size()：获取当前集合中实际存储的元素个数
（4）boolean isEmpty()：判断当前集合是否为空集合
（5）boolean contains(Object obj)：判断当前集合中是否存在一个与obj对象equals返回true的元素
（6）boolean containsAll(Collection coll)：判断coll集合中的元素是否在当前集合中都存在。即coll集合是否是当前集合的“子集”
（7）boolean equals(Object obj)：判断当前集合与obj是否相等

### 2.3 删除

（8）void clear()：清空集合元素
（9） boolean remove(Object obj) ：从当前集合中删除第一个找到的与obj对象equals返回true的元素。
（10）boolean removeAll(Collection coll)：从当前集合中删除所有与coll集合中相同的元素。即this = this - this ∩ coll
（11）boolean retainAll(Collection coll)：从当前集合中删除两个集合中不同的元素，使得当前集合仅保留与coll集合中的元素相同的元素，即当前集合中仅保留两个集合的交集，即**this  = this ∩ coll**（即会直接操作调用此方法的对象）

### 2.4 其它

（12）Object[] toArray()：返回包含当前集合中所有元素的数组
（13）hashCode()：获取集合对象的哈希值
（14）iterator()：返回迭代器对象，用于集合遍历

## 3. Iterator(迭代器)接口

### 3.1 Iterator接口

- 在程序开发中，经常需要遍历集合中的所有元素。针对这种需求，JDK专门提供了一个接口`java.util.Iterator`。
- `Iterator`接口也是Java集合中的一员，但它与`Collection`、`Map`接口有所不同。
  - Collection接口与Map接口主要用于`存储`元素
  - `Iterator`，被称为迭代器接口，本身并不提供存储对象的能力，主要用于`遍历`**Collection**中的元素

- Collection接口继承了java.lang.Iterable接口，该接口有一个iterator()方法，**所有实现了Collection接口的集合类都有一个iterator()方法**，用以返回一个实现了Iterator接口的对象。
  - `public Iterator iterator()`: 获取集合对应的迭代器，用来遍历集合中的元素的。
  - 集合对象每次调用iterator()方法都得到一个全新的迭代器对象，默认游标都在集合的第一个元素之前。
- Iterator接口的常用方法如下：
  - `public E next()`:返回迭代的下一个元素。
  - `public boolean hasNext()`:如果仍有元素可以迭代，则返回 true。
- 注意：在调用it.next()方法之前必须要调用it.hasNext()进行检测。若不调用，且下一条记录无效，直接调用it.next()会抛出`NoSuchElementException异常`。

```java
public class TestIterator {
    public void test(){
        Collection coll = new ArrayList();
        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");

        Iterator iterator = coll.iterator();//获取迭代器对象
        while(iterator.hasNext()) {//判断是否还有元素可迭代
            System.out.println(iterator.next());//取出下一个元素
        }
    }
}
```

### 3.2 迭代器的执行原理

Iterator迭代器对象在遍历集合时，内部采用指针的方式来跟踪集合中的元素，接下来通过一个图例来演示Iterator对象迭代元素的过程：

![image-20220407235130988](http://jason243.online/javase_songhongkang/images/image-20220407235130988.png)

### 3.3 使用Iterator迭代器删除元素

java.util.Iterator迭代器中有一个方法：void remove() ，注意：

- Iterator可以删除集合的元素，但是遍历过程中通过迭代器对象的remove方法，不是集合对象的remove方法。
- 如果还未调用next()或在上一次调用 next() 方法之后已经调用了 remove() 方法，再调用remove()都会报IllegalStateException。
- Collection已经有remove(xx)方法了，为什么Iterator迭代器还要提供删除方法呢？因为迭代器的remove()可以按指定的条件进行删除。

例如：要删除以下集合元素中的偶数

```java
package com.atguigu.iterator;

import org.junit.Test;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;

public class TestIteratorRemove {
    @Test
    public void test01(){
        Collection coll = new ArrayList();
        coll.add(1);
        coll.add(2);
        coll.add(3);
        coll.add(4);
        coll.add(5);
        coll.add(6);

        Iterator iterator = coll.iterator();
        while(iterator.hasNext()){
            Integer element = (Integer) iterator.next();
            if(element % 2 == 0){
                iterator.remove();
            }
        }
        System.out.println(coll);
    }
}

```

在JDK8.0时，Collection接口有了removeIf 方法，即可以根据条件删除。（第18章中再讲）

```java
package com.atguigu.collection;

import org.junit.Test;

import java.util.ArrayList;
import java.util.Collection;
import java.util.function.Predicate;

public class TestCollectionRemoveIf {
    @Test
    public void test01(){
        Collection coll = new ArrayList();
        coll.add("小李广");
        coll.add("扫地僧");
        coll.add("石破天");
        coll.add("佛地魔");
        System.out.println("coll = " + coll);

        coll.removeIf(new Predicate() {
            @Override
            public boolean test(Object o) {
                String str = (String) o;
                return str.contains("地");
            }
        });
        System.out.println("删除包含\"地\"字的元素之后coll = " + coll);
    }
}
```

### 3.4 foreach循环（底层实现为Interator）

- foreach循环（也称增强for循环）是 JDK5.0 中定义的一个高级for循环，专门用来`遍历数组和集合`的。

- 它用于遍历Collection和数组。通常只进行遍历元素，不要在遍历的过程中对集合元素进行增删操作。
  - 练习：判断输出结果为何？

```java
public class ForTest {
    public static void main(String[] args) {
        String[] str = new String[5];
        for (String myStr : str) {
            myStr = "atguigu";	// 只改变了 mystr 局部变量，与String不可变无关，换int[]也这样
            System.out.println(myStr);
        }
        for (int i = 0; i < str.length; i++) {
            System.out.println(str[i]);	// null
        }
    }
}
```

## 4. Collection子接口1：List

### 4.1 List接口特点

- List集合类中`元素有序`、且`可重复`，集合中的每个元素都有其对应的顺序索引。

- JDK API中List接口的实现类常用的有：`ArrayList`、`LinkedList`和`Vector`。

### 4.2 List接口方法

List除了从Collection集合继承的方法外，List 集合里添加了一些`根据索引`来操作集合元素的方法。

- 插入元素
  - `void add(int index, Object ele)`：在index位置插入ele元素
  - `boolean addAll(int index, Collection eles)`: 从index位置开始将eles中的所有元素添加进来
- 获取元素
  - `Object get(int index)`: 获取指定index位置的元素
  - `List subList(int fromIndex, int toIndex)` : 返回从fromIndex到toIndex位置的子集合
- 获取元素索引
  - `int indexOf(Object obj)` : 返回obj在集合中首次出现的位置
  - `int lastIndexOf(Object obj)` : 返回obj在当前集合中末次出现的位置
- 删除和替换元素
  - `Object remove(int index)`: 移除指定index位置的元素，并返回此元素
  - `Object set(int index, Object ele)`: 设置指定index位置的元素为ele

> 注意：在JavaSE中List名称的类型有两个，一个是java.util.List集合接口，一个是java.awt.List图形界面的组件，别导错包了。

### 4.3 List接口主要实现类：ArrayList

- ArrayList 是 List 接口的`主要实现类`
- 本质上，ArrayList是对象引用的一个”变长”数组
- Arrays.asList(…) 方法返回的 List 集合，既不是 ArrayList 实例，也不是 Vector 实例。 Arrays.asList(…) 返回值是一个固定长度的 List 集合

### 4.4 List的实现类之二：LinkedList

- 对于频繁的插入或删除元素的操作，建议使用LinkedList类，效率较高。这是由底层采用链表（双向链表）结构存储数据决定的。（其他时候优先ArrayList，实践证明在业务中效率更高，LinkedList在算法题用的更多）

- 特有方法：
  - void addFirst(Object obj)
  - void addLast(Object obj)	
  - Object getFirst()
  - Object getLast()
  - Object removeFirst()
  - Object removeLast()

### 4.5 List的实现类之三：Vector

- Vector 是一个`古老`的集合，JDK1.0就有了。大多数操作与ArrayList相同，区别之处在于Vector是`线程安全`的。
- 在各种List中，最好把`ArrayList作为默认选择`。当插入、删除频繁时，使用LinkedList；Vector总是比ArrayList慢，所以尽量避免使用。
- 特有方法：
  - void addElement(Object obj)
  - void insertElementAt(Object obj,int index)
  - void setElementAt(Object obj,int index)
  - void removeElement(Object obj)
  - void removeAllElements()

### 4.6 ArrayList与Vector对比与底层实现介绍

它们的底层物理结构都是数组，我们称为动态数组。

- 底层实现
  - ArrayList是新版的动态数组，线程不安全，效率高
  - Vector是旧版的动态数组，线程安全，效率低。
- 扩容机制：动态数组的扩容机制不同
  - ArrayList默认扩容为原来的1.5倍
  - Vector默认扩容增加为原来的2倍。
- 数组的默认初始化容量
  - 那么Vector的内部数组的初始容量默认为10
  - ArrayList在JDK 6.0 及之前的版本也是10，JDK8.0 之后的版本ArrayList初始化为长度为0的空数组，在添加第一个元素时，再创建长度为10的数组（节约一点空间）

## 5. Collection子接口2：Set

### 5.0 Set与Map的关系介绍（Set内部是Map）

Set的内部实现其实是一个Map，Set中的元素，存储在HashMap的key中。即HashSet的内部实现是一个HashMap，TreeSet的内部实现是一个TreeMap，LinkedHashSet的内部实现是一个LinkedHashMap。

### 5.1 Set接口概述

- Set接口是Collection的子接口，Set接口相较于Collection接口没有提供额外的方法
- Set 集合**不允许包含相同的元素**，如果试把两个相同的元素加入同一个 Set 集合中，则添加操作失败。
- Set集合支持的遍历方式和Collection集合一样：foreach和Iterator。
- Set的常用实现类有：HashSet、TreeSet、LinkedHashSet。

### 5.2 Set主要实现类：HashSet

#### 5.2.1 HashSet概述

- **HashSet 是 Set 接口的主要实现类，大多数时候使用 Set 集合时都使用这个实现类。**
- HashSet 按 Hash 算法来存储集合中的元素，因此具有很好的存储、查找、删除性能。
- HashSet 具有以下`特点`：
  - **不能保证元素的排列顺序**（无序性来源于按hash值存放）
  - **HashSet 不是线程安全的**
  - **集合元素可以是 null**
- HashSet 集合`判断两个元素相等的标准`：两个对象通过 `hashCode()` 方法得到的**哈希值相等**，并且两个对象的 **`equals() `方法返回值为true**。
- 对于存放在Set容器中的对象，**对应的类一定要重写hashCode()和equals(Object obj)方法**，以实现对象相等规则

#### 5.2.2 HashSet中添加元素的过程：

- 第1步：调用 hashCode() 方法得到该对象的 hashCode值，然后通过散列函数决定该对象在 HashSet 底层数组中的存储位置。

- 第2步：如果要在数组中存储的位置上没有元素，则直接添加成功。

- 第3步：如果要在数组中存储的位置上有元素，则继续比较：

  - 如果两个元素的hashCode值不相等，则添加成功；
  - 如果两个元素的hashCode()值相等，则会继续调用equals()方法：
    - 如果equals()方法结果为false，则添加成功。
    - 如果equals()方法结果为true，则添加失败。

  > 添加失败只是不添加，不会报错

#### 5.2.3 重写 hashCode() 方法的基本原则

- 在程序运行时，同一个对象多次调用 hashCode() 方法应该返回相同的值。
- 当两个对象的 equals() 方法比较返回 true 时，这两个对象的 hashCode() 方法的返回值也应相等。
- 对象中所有可以equals比较的字段都应该作为hash值计算的一部分

> 注意：如果两个元素的 equals() 方法返回 true，但它们的 hashCode() 返回值不相等，hashSet 将会把它们存储在不同的位置，但依然可以添加成功。

#### 5.2.4 重写equals()方法的基本原则

- 重写equals方法的时候一般都需要同时复写hashCode方法。通常参与计算hashCode的对象的属性也应该参与到equals()中进行计算。

- 推荐：开发中直接调用Eclipse/IDEA里的快捷键自动重写equals()和hashCode()方法即可。

  - 为什么用Eclipse/IDEA复写hashCode方法，有31这个数字？

  ```
  首先，选择系数的时候要选择尽量大的系数。因为如果计算出来的hash地址越大，所谓的“冲突”就越少，查找起来效率也会提高。（减少冲突）
  
  其次，31只占用5bits,相乘造成数据溢出的概率较小。
  
  再次，31可以 由i*31== (i<<5)-1来表示,现在很多虚拟机里面都有做相关优化。（提高算法效率）
  
  最后，31是一个素数，素数作用就是如果我用一个数字来乘以这个素数，那么最终出来的结果只能被素数本身和被乘数还有1来整除！(减少冲突)
  ```

#### 5.2.5 面试辨析题

其中Person类中重写了hashCode()和equal()方法

```java
HashSet set = new HashSet();
Person p1 = new Person(1001,"AA");
Person p2 = new Person(1002,"BB");

set.add(p1);
set.add(p2);
p1.name = "CC";
// 此时传入p1会计算hash，hash计算要包含所有可以equals的字段，所以算出来的hash变了，remove失败
set.remove(p1);	
System.out.println(set); // [Person{id=1002, name='BB'}, Person{id=1001, name='CC'}]

set.add(new Person(1001,"CC")); // equals为false，新new的对象，只是内部的成员变量值一样而已
// 输出：[Person{id=1002, name='BB'}, Person{id=1001, name='CC'}, Person{id=1001, name='CC'}]
System.out.println(set); 

set.add(new Person(1001,"AA")); // equals为false，新new的对象，只是内部的成员变量值一样而已
// 输出：[Person{id=1002, name='BB'}, Person{id=1001, name='CC'}, Person{id=1001, name='CC'}, Person{id=1001, name='AA'}]
System.out.println(set);
```

### 5.3 Set实现类之二：LinkedHashSet

- LinkedHashSet 是 HashSet 的子类，不允许集合元素重复。
- LinkedHashSet 根据元素的 hashCode 值来决定元素的存储位置，但它同时使用`双向链表`维护元素的次序，这使得元素看起来是以`添加顺序`保存的。
- LinkedHashSet`插入性能略低`于 HashSet，但在`迭代访问` Set 里的全部元素时有很好的性能。

### 5.4 Set实现类之三：TreeSet

#### 5.4.1 TreeSet概述

- TreeSet 是 SortedSet 接口的实现类，TreeSet 可以按照添加的元素的指定的属性的大小顺序进行遍历。
- TreeSet底层使用`红黑树`结构存储数据
- 新增的方法如下： (了解)
  - Comparator comparator()
  - Object first()
  - Object last()
  - Object lower(Object e)
  - Object higher(Object e)
  - SortedSet subSet(fromElement, toElement)
  - SortedSet headSet(toElement)
  - SortedSet tailSet(fromElement)
- TreeSet特点：不允许重复、实现排序（自然排序或定制排序，默认情况下，TreeSet 采用自然排序）
- 因为只有相同类的两个实例才会比较大小，所以向 TreeSet 中添加的应该是`同一个类的对象`。
- 对于 TreeSet 集合而言，它判断`两个对象是否相等的唯一标准`是：两个对象通过 `compareTo(Object obj) 或compare(Object o1,Object o2)`方法比较返回值。返回值为0，则认为两个对象相等。

## 6. Map接口

### 6.1 Map接口概述

- Map与Collection并列存在。用于保存具有`映射关系`的数据：key-value

  - `Collection`集合称为单列集合，元素是孤立存在的（理解为单身）。
  - `Map`集合称为双列集合，元素是成对存在的(理解为夫妻)。

- Map 中的 key 和  value 都可以是任何引用类型的数据。但常用String类作为Map的“键”。

- Map接口的常用实现类：`HashMap`、`LinkedHashMap`、`TreeMap`和``Properties`。其中，**HashMap是 Map 接口使用`频率最高`的实现类**。

  <img src="http://jason243.online/javase_songhongkang/images/image-20220409001015034.png" alt="image-20220409001015034" style="zoom:67%;" />

### 6.2 Map中key-value特点

- Map 中的 `key用Set来存放`，`不允许重复`，即同一个 Map 对象所对应的类，须重写hashCode()和equals()方法

  <img src="http://jason243.online/javase_songhongkang/images/image-20220514190412763.png" alt="image-20220514190412763" style="zoom:67%;" />

- key 和 value 之间存在单向一对一关系，即通过指定的 key 总能找到唯一的、确定的 value，不同key对应的`value可以重复`。value所在的类要重写equals()方法。

- key和value构成一个entry。所有的entry彼此之间是`无序的`、`不可重复的`。

### 6.2 Map接口的常用方法

- **添加、修改操作：**
  - Object put(Object key,Object value)：将指定key-value添加到(或修改)当前map对象中
  - void putAll(Map m):将m中的所有key-value对存放到当前map中
- **删除操作：**
  - Object remove(Object key)：移除指定key的key-value对，并返回value
  - void clear()：清空当前map中的所有数据
- **元素查询的操作：**
  - Object get(Object key)：获取指定key对应的value
  - boolean containsKey(Object key)：是否包含指定的key
  - boolean containsValue(Object value)：是否包含指定的value
  - int size()：返回map中key-value对的个数
  - boolean isEmpty()：判断当前map是否为空
  - boolean equals(Object obj)：判断当前map和参数对象obj是否相等
- **元视图操作的方法：**
  - Set keySet()：返回所有key构成的Set集合
  - Collection values()：返回所有value构成的Collection集合
  - Set entrySet()：返回所有key-value对构成的Set集合



### 6.3 Map的主要实现类：HashMap

#### 6.3.1 HashMap概述

- HashMap是 Map 接口`使用频率最高`的实现类。
- HashMap是**线程不安全**的。**允许添加 null 键和 null 值**。
- 存储数据采用的哈希表结构，底层使用`一维数组`+`单向链表`+`红黑树`进行key-value数据的存储。与HashSet一样，元素的存取顺序不能保证一致。
- HashMap `判断两个key相等的标准`是：两个 key 的hashCode值相等，通过 equals() 方法返回 true。
- HashMap `判断两个value相等的标准`是：两个 value 通过 equals() 方法返回 true。

#### 6.3.2 HashMap与HashTable在Java8中的物理结构介绍

HashMap和Hashtable底层都是哈希表（也称散列表），其中维护了一个长度为**2的幂次方**的Entry类型的数组table，数组的每一个索引位置被称为一个桶(bucket)，你添加的映射关系(key,value)最终都被封装为一个Map.Entry类型的对象，放到某个table[index]桶中。

<img src="http://jason243.online/javase_songhongkang/images/image-20221029144811305.png" alt="image-20221029144811305" style="zoom:80%;" />

#### 6.3.3 HashMap的底层实现介绍以及Java8与Java7的实现区别对比

- ① jdk8使用HashMap()的构造器创建对象时，并没有在底层初始化长度为16的table数组。
- ② jdk8中添加的key,value封装到了HashMap.Node类的对象中。而非jdk7中的HashMap.Entry。
- ③ **jdk8**中新增的元素所在的索引位置如果有其他元素。在经过一系列判断后，如果能添加，则是**旧的元素指向新**的元素。而非**jdk7**中的**新的元素指向旧的元素**。（“七上八下”）
- ④ jdk7时底层的数据结构是：数组+单向链表。 而jdk8时，底层的数据结构是：数组+单向链表+红黑树。
  - 红黑树出现的时机：当某个索引位置i上的链表的长度达到8，且数组的长度超过64时，此索引位置上的元素要从单向链表改为红黑树。
  - 如果索引i位置是红黑树的结构，当不断删除元素的情况下，当前索引i位置上的元素的个数低于6时，要从红黑树改为单向链表。



### 6.4 Map实现类之二：LinkedHashMap

- LinkedHashMap 是 HashMap 的子类

- 存储数据采用的哈希表结构+链表结构，在HashMap存储结构的基础上，使用了一对`双向链表`来`记录添加元素的先后顺序`，可以保证遍历元素时，与添加的顺序一致。

- 通过哈希表结构可以保证键的唯一、不重复，需要键所在类重写hashCode()方法、equals()方法。

  > 用来实现LRU算法很方便



### 6.5 Map实现类之三：TreeMap

- TreeMap存储 key-value 对时，需要根据 key-value 对进行排序。TreeMap 可以保证所有的 key-value 对处于`有序状态`。
- TreeSet底层使用`红黑树`结构存储数据
- TreeMap 的 Key 的排序：
  - `自然排序`：TreeMap 的所有的 Key 必须实现 Comparable 接口，而且所有的 Key 应该是同一个类的对象，否则将会抛出 ClasssCastException
  - `定制排序`：创建 TreeMap 时，构造器传入一个 Comparator 对象，该对象负责对 TreeMap 中的所有 key 进行排序。此时不需要 Map 的 Key 实现 Comparable 接口
- TreeMap判断`两个key相等的标准`：两个key通过compareTo()方法或者compare()方法返回0。



### 6.6 Map实现类之四：Hashtable

- Hashtable是Map接口的`古老实现类`，JDK1.0就提供了。不同于HashMap，Hashtable是线程安全的。
- Hashtable实现原理和HashMap相同，功能相同。底层都使用哈希表结构（数组+单向链表），查询速度快。
- 与HashMap一样，Hashtable 也不能保证其中 Key-Value 对的顺序
- Hashtable判断两个key相等、两个value相等的标准，与HashMap一致。
- 与HashMap不同，Hashtable 不允许使用 null 作为 key 或 value。

**面试题：Hashtable和HashMap的区别**

- HashMap:底层是一个哈希表（jdk7:数组+链表;jdk8:数组+链表+红黑树）,是一个线程不安全的集合,执行效率高
  Hashtable:底层也是一个哈希表（数组+链表）,是一个线程安全的集合,执行效率低

- HashMap集合:可以存储null的键、null的值
  Hashtable集合,不能存储null的键、null的值
- Hashtable和Vector集合一样,在jdk1.2版本之后被更先进的集合(HashMap,ArrayList)取代了。所以HashMap是Map的主要实现类，Hashtable是Map的古老实现类。
- Hashtable的子类Properties（配置文件）依然活跃在历史舞台
  Properties集合是一个唯一和IO流相结合的集合



### 6.7 Map实现类之五：Properties（Hashtable子类）

- Properties 类是 Hashtable 的子类，该对象用于处理属性文件
- 由于属性文件里的 key、value 都是字符串类型，所以 Properties 中要求 key 和 value 都是字符串类型
- 存取数据时，建议使用setProperty(String key,String value)方法和getProperty(String key)方法

```java
@Test
public void test01() {
    Properties properties = System.getProperties();
    String fileEncoding = properties.getProperty("file.encoding");//当前源文件字符编码
    System.out.println("fileEncoding = " + fileEncoding);
}
@Test
public void test02() {
    Properties properties = new Properties();
    properties.setProperty("user","songhk");
    properties.setProperty("password","123456");
    System.out.println(properties);
}

@Test
public void test03() throws IOException {
    Properties pros = new Properties();
    pros.load(new FileInputStream("jdbc.properties"));
    String user = pros.getProperty("user");
    System.out.println(user);
}
```



### 6.8 【拓展】HashMap的相关问题

#### 1、说说你理解的哈希算法

hash算法是一种可以从任何数据中提取出其“指纹”的数据摘要算法，它将任意大小的数据映射到一个固定大小的序列上，这个序列被称为hash code、数据摘要或者指纹。比较出名的hash算法有MD5、SHA。hash是具有唯一性且不可逆的，唯一性是指相同的“对象”产生的hash code永远是一样的。

#### 2、Entry中的hash属性为什么不直接使用key的hashCode()返回值呢？

不管是JDK1.7还是JDK1.8中，都不是直接用key的hashCode值直接与table.length-1计算求下标的，而是先对key的hashCode值进行了一个运算，JDK1.7和JDK1.8关于hash()的实现代码不一样，但是不管怎么样都是为了提高hash code值与 (table.length-1)的按位与完的结果，尽量的均匀分布。

![image-20220514190454633](http://jason243.online/javase_songhongkang/images/image-20220514190454633-1661448231965.png)

JDK1.7：

```java
    final int hash(Object k) {
        int h = hashSeed;
        if (0 != h && k instanceof String) {
            return sun.misc.Hashing.stringHash32((String) k);
        }

        h ^= k.hashCode();
        h ^= (h >>> 20) ^ (h >>> 12);
        return h ^ (h >>> 7) ^ (h >>> 4);
    }

```

JDK1.8：

```java
	static final int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    }

```

虽然算法不同，但是思路都是将hashCode值的高位二进制与低位二进制值进行了异或，然高位二进制参与到index的计算中。

为什么要hashCode值的二进制的高位参与到index计算呢？

因为一个HashMap的table数组一般不会特别大，至少在不断扩容之前，那么table.length-1的大部分高位都是0，直接用hashCode和table.length-1进行&运算的话，就会导致总是只有最低的几位是有效的，那么就算你的hashCode()实现的再好也难以避免发生碰撞，这时让高位参与进来的意义就体现出来了。它对hashcode的低位添加了随机性并且混合了高位的部分特征，显著减少了碰撞冲突的发生。

#### 3、HashMap是如何决定某个key-value存在哪个桶的呢？

因为hash值是一个整数，而数组的长度也是一个整数，有两种思路：

①hash 值 % table.length会得到一个[0,table.length-1]范围的值，正好是下标范围，但是用%运算效率没有位运算符&高。

②hash 值 & (table.length-1)，任何数 & (table.length-1)的结果也一定在[0, table.length-1]范围。

![1563800372286](http://jason243.online/javase_songhongkang/images/1563800372286-1661448231966.png)

#### 4、为什么要保持table数组一直是2的n次幂呢？

因为如果数组的长度为2的n次幂，那么table.length-1的二进制就是一个高位全是0，低位全是1的数字，这样才能保证每一个下标位置都有机会被用到（因为底层实现确定位置用的位&）

#### 5、解决[index]冲突问题

虽然从设计hashCode()到上面HashMap的hash()函数，都尽量减少冲突，但是仍然存在两个不同的对象返回的hashCode值相同，或者hashCode值就算不同，通过hash()函数计算后，得到的index也会存在大量的相同，因此key分布完全均匀的情况是不存在的。那么发生碰撞冲突时怎么办？

JDK1.8之间使用：数组+链表的结构。

![1563802656661](http://jason243.online/javase_songhongkang/images/1563802656661-1661448231966.png)

JDK1.8之后使用：数组+链表/红黑树的结构。

![1563802665708](http://jason243.online/javase_songhongkang/images/1563802665708-1661448231966.png)

即hash相同或hash&(table.lengt-1)的值相同，那么就存入同一个“桶”table[index]中，使用链表或红黑树连接起来。

#### 6、为什么JDK1.8会出现红黑树和链表共存呢？

因为当冲突比较严重时，table[index]下面的链表就会很长，那么会导致查找效率大大降低，而如果此时选用二叉树可以大大提高查询效率。

但是二叉树的结构又过于复杂，占用内存也较多，如果结点个数比较少的时候，那么选择链表反而更简单。所以会出现红黑树和链表共存。

#### 7、加载因子的值大小有什么关系？

> 加载因子是决定哈希表什么时候扩容（阈值大小）的一个系数
>
> 阈值（threshold）= 哈希表当前容量（capacity） × 加载因子（loadFactor）

如果太大，threshold就会很大，那么如果冲突比较严重的话，就会导致table[index]下面的结点个数很多，影响效率。

如果太小，threshold就会很小，那么数组扩容的频率就会提高，数组的使用率也会降低，那么会造成空间的浪费。

#### 8、什么时候树化？什么时候反树化？

```java
static final int TREEIFY_THRESHOLD = 8;//树化阈值
static final int UNTREEIFY_THRESHOLD = 6;//反树化阈值
static final int MIN_TREEIFY_CAPACITY = 64;//最小树化容量
```

- 当某table[index]下的链表的结点个数达到8，并且table.length>=64，那么如果新Entry对象还添加到该table[index]中，那么就会将table[index]的链表进行树化。
- 当某table[index]下的红黑树结点个数少于6个，此时，
  - 当继续删除table[index]下的树结点，最后这个根结点的左右结点有null，或根结点的左结点的左结点为null，会反树化
  - 当重新添加新的映射关系到map中，导致了map重新扩容了，这个时候如果table[index]下面还是小于等于6的个数，那么会反树化

#### 9、key-value中的key是否可以修改？

不可以。删了原来的再加入新的。key-value存储到HashMap中会存储key的hash值，这样就不用在每次查找时重新计算每一个Entry或Node（TreeNode）的hash值了，因此如果已经put到Map中的key-value，再修改key的属性，而这个属性又参与hashcode值的计算，那么会导致匹配不上。

这个规则也同样适用于LinkedHashMap、HashSet、LinkedHashSet、Hashtable等所有散列存储结构的集合。

#### 10、JDK1.7中HashMap的循环链表是怎么回事？如何解决？

![HashMap的循环引用问题](http://jason243.online/javase_songhongkang/images/HashMap的循环引用问题.jpg)

- JDK7中的出现原因（多线程情况下）：

1. **头插法反转链表**
   JDK 1.7 的 HashMap 在插入链表节点时使用 **头插法**（新节点插入链表头部），扩容迁移之后**链表顺序会被反转**。例如：
   - 原链表顺序：A → B → C
   - 迁移后顺序：C → B → A
2. **多线程并发扩容**
   当两个线程同时触发扩容（如 `put()` 操作导致 `size > threshold`），且操作同一链表时：
   - **线程1** 开始迁移链表，刚处理完节点 A（新链表指向 A）。
   - **线程2** 抢到 CPU 时间片，完成整个链表的迁移，新链表变为 C → B → A。
   - **线程1** 恢复执行时，仍按旧链表的顺序继续迁移后续节点，此时节点 B 的 `next` 指向 A，而线程2已修改为 A 的 `next` 指向 B，最终形成 **A → B → A** 的死循环。

- 避免HashMap发生死循环的常用解决方案：
  - 多线程环境下，使用线程安全的ConcurrentHashMap替代HashMap，推荐
  - 多线程环境下，使用synchronized或Lock加锁，但会影响性能，不推荐
  - 多线程环境下，使用线程安全的Hashtable替代，性能低，不推荐

- HashMap死循环只会发生在JDK1.7版本中，主要原因：头插法+链表+多线程并发+扩容。

- 在JDK1.8中，HashMap改用**尾插法**，解决了链表死循环的问题。



## 7. Collections工具类

参考操作数组的工具类：Arrays，Collections 是一个操作 Set、List 和 Map 等集合的工具类。

### 7.1 常用方法

Collections 中提供了一系列**静态**的方法对集合元素进行排序、查询和修改等操作，还提供了对集合对象设置不可变、对集合对象实现同步控制等方法（均为static方法）：

**排序操作：**

- reverse(List)：反转 List 中元素的顺序
- shuffle(List)：对 List 集合元素进行随机排序
- sort(List)：根据元素的自然顺序对指定 List 集合元素按升序排序
- sort(List，Comparator)：根据指定的 Comparator 产生的顺序对 List 集合元素进行排序
- swap(List，int， int)：将指定 list 集合中的 i 处元素和 j 处元素进行交换

**查找**

- Object max(Collection)：根据元素的自然顺序，返回给定集合中的最大元素
- Object max(Collection，Comparator)：根据 Comparator 指定的顺序，返回给定集合中的最大元素
- Object min(Collection)：根据元素的自然顺序，返回给定集合中的最小元素
- Object min(Collection，Comparator)：根据 Comparator 指定的顺序，返回给定集合中的最小元素
- int binarySearch(List list, T key)在List集合中查找某个元素的下标，但是List的元素必须是T或T的子类对象，而且必须是可比较大小的，即支持自然排序的。而且集合也事先必须是有序的，否则结果不确定。
- int binarySearch(List list, T key, Comparator c)在List集合中查找某个元素的下标，但是List的元素必须是T或T的子类对象，而且集合也事先必须是按照c比较器规则进行排序过的，否则结果不确定。
- int frequency(Collection c，Object o)：返回指定集合中指定元素的出现次数

**复制、替换**

- void copy(List dest, List src)：将src中的内容复制到dest中
- boolean replaceAll(List list，Object oldVal，Object newVal)：使用新值替换 List 对象的所有旧值
- 提供了多个unmodifiableXxx()方法，该方法返回指定 Xxx的不可修改的视图。

**添加**

- boolean addAll(Collection  c, T... elements)将所有指定元素添加到指定 collection 中。

**同步**

- Collections 类中提供了多个 synchronizedXxx() 方法，该方法可使将指定集合包装成线程同步的集合，从而可以解决多线程并发访问集合时的线程安全问题：

![image-20220409003002526](http://jason243.online/javase_songhongkang/images/image-20220409003002526.png)



## 8、其他相关内容补充

### 8.1 栈与队列的对比介绍

------

#### **8.1.1 栈（Stack）**

**特点**：  

- **先进后出（FILO）**  ：最后压入的元素最先弹出。
- **核心操作**：仅在栈顶（一端）进行插入（`push`）和删除（`pop`）。

**常用方法**：  

| 方法        | 作用                   | 示例（Java）               |
| ----------- | ---------------------- | -------------------------- |
| `push(E e)` | 压入元素到栈顶         | `stack.push(1);`           |
| `pop()`     | 移除并返回栈顶元素     | `int top = stack.pop();`   |
| `peek()`    | 查看栈顶元素（不移除） | `int top = stack.peek();`  |
| `isEmpty()` | 判断栈是否为空         | `if(stack.isEmpty()){...}` |

**具体实现**：  

1. **`Stack`类**（Java旧版）：  

```java
   Stack<Integer> stack = new Stack<>();
```

- 基于数组实现，但线程安全（性能较低，已不推荐使用）。  

2. **`Deque`接口的替代方案**（推荐）：  

```java
   Deque<Integer> stack = new ArrayDeque<>(); // 数组实现（默认）
   Deque<Integer> stack = new LinkedList<>(); // 链表实现
```

- 使用`push()`、`pop()`、`peek()`方法操作栈。  

**时间复杂度**：插入/删除均为 **O(1)**  ，搜索/索引为 **O(n)**。  
**应用场景**：函数调用栈、括号匹配、表达式求值（如逆波兰表达式）。

#### **8.1.2 队列（Queue）**

**特点**：  

- **先进先出（FIFO）**  ：最早入队的元素最先出队。  
- **核心操作**：队尾插入（`offer`/`add`），队头删除（`poll`/`remove`）。  

**常用方法**：  

| 方法         | 作用                         | 示例（Java）                 |
| ------------ | ---------------------------- | ---------------------------- |
| `offer(E e)` | 入队（队尾插入，不抛异常）   | `queue.offer(1);`            |
| `poll()`     | 出队（队头移除，不抛异常）   | `int head = queue.poll();`   |
| `peek()`     | 查看队头元素（不移除）       | `int head = queue.peek();`   |
| `add(E e)`   | 入队（队尾插入，失败抛异常） | `queue.add(1);`              |
| `remove()`   | 出队（队头移除，失败抛异常） | `int head = queue.remove();` |

**具体实现**：  

1. **`LinkedList`**：  

```java
   Queue<Integer> queue = new LinkedList<>();
```

- 基于链表实现，支持动态扩容。  

2. **`ArrayDeque`**：  

```java
   Queue<Integer> queue = new ArrayDeque<>();
```

- 基于数组实现（循环队列），性能优于`LinkedList`。  

3. **`PriorityQueue`**（优先队列）：  

```java
   Queue<Integer> queue = new PriorityQueue<>();
```

- 元素按优先级出队（默认小顶堆），需自定义排序规则时传入`Comparator`。  

**时间复杂度**：插入/删除均为 **O(1)**  （优先队列插入为 **O(log n)**  ）。  
**应用场景**：任务调度、广度优先搜索（BFS）、消息队列。

#### **8.1.3 对比总结**

| 结构 | 原则 | 核心方法                      | 推荐实现类                |
| ---- | ---- | ----------------------------- | ------------------------- |
| 栈   | FILO | `push()`, `pop()`, `peek()`   | `ArrayDeque`              |
| 队列 | FIFO | `offer()`, `poll()`, `peek()` | `ArrayDeque`/`LinkedList` |

**使用建议**：  

- **栈**：优先用`ArrayDeque`（高效、无同步开销）。  
- **队列**：普通队列用`ArrayDeque`，需优先级时用`PriorityQueue`。