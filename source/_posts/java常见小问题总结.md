---
title: java常见小问题总结
abbrlink: e2e7f88
date: 2021-07-03 19:17:09
updated:
tags:
categories:
keywords:
description:
top_img:
comments:
cover:
toc:
toc_number:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

# 总结

### Stringbuffer

demo:

```java
/**
 * @author runrab
 */
public class Test {
    public static void main(String[] args) {
        StringBuffer a = new StringBuffer("A");
        StringBuffer b = new StringBuffer("B");
        System.out.println(a);
        operator(a,b);
        System.out.println(a+","+b);
    }
    public static void operator(StringBuffer x,StringBuffer y){
        x.append(y);
        y=x;
       // x的值分配给'y'是从未使用过
        //'x' 可能不应分配给 'y'
    }
}
```

就是说这y=x;根本就没起作用。

![Snipaste_2021-06-27_16-19-44](https://cdn.jsdelivr.net/gh/hs-p/images@master/img/2021/06/2720210627162151.png)

### 2：java中 String a=new String("1"+"2")创建了几个对象

2个：a值和a引用地址，也叫引用对象。**一个是"1"+"2" 创建后就会放入常量池中，一个是new String()。**

引用变量和对象，对象一般通过new在堆中创建，s只是一个引用变量。

所有的字符串都是String对象，由于字符串文字的大量使用，java中为了节省时间，在编译阶段，会把字符串文字放在文字池中，文字池的一个好处就是可以把相同的字符串合并，占用一个空间，我们可以用==判断一下两个引用变量是否指向了一个地址即一个对象。

### 3String str=”aaa”,与String str=new String(“aaa”)一样吗？

一共有两个引用，三个对象。因为”aa”与”bb”都是常量，常量的值不能改变，当执行字符串拼接时候，
会创建一个新的常量是” aabbb”,有将其存到常量池中。

### 4StringString StringBuffffer 和 StringBuilder 的区别是什

么？
String是只读字符串，它并不是基本数据类型，而是一个对象。从底层源码来看是一个fifinal类型的字
符
数组，所引用的字符串不能被改变，一经定义，无法再增删改。每次对String的操作都会生成新的
String对象

```
private final char value[];
```

**每次+操作 ： 隐式在堆上new了一个跟原字符串相同的StringBuilder对象，再调用append方法 拼接**
**+后面的字符。**
StringBuffer与StringBuilder都继承了AbstractStringBulder类，而AbtractStringBuilder又实现了
CharSequence接口，两个类都是用来进行字符串操作的。
在做字符串拼接修改删除替换时，效率比string更高。
StringBuffer是线程安全的，Stringbuilder是非线程安全的。所以Stringbuilder比stringbuffer效率更
高，StringBuffer的方法大多都加了synchronized关键字

### 5Hashcode的作用

java的集合有两类，一类是List，还有一类是Set。**前者有序可重复，后者无序不重复。**当我们在set中
插入的时候怎么判断是否已经存在该元素呢，可以通过**equals方法**。但是如果元素太多，用这样的方法
就会比较满。
于是有人发明了**哈希算法来提高集合中查找元素的效率**。 这种方式将集合分成若干个存储区域，每个对
象可以计算出一个**哈希码**，可以将**哈希码分组**，每组分别对应某个存储区域，根据一个对象的哈希码就
可以确定该对象应该存储的那个区域。
hashCode方法可以这样理解：**它返回的就是根据对象的内存地址换算出的一个值**。这样一来，当集合
要添加新的元素时，**先调用这个元素的hashCode方法**，就一下子能定位到它应该放置的物理位置上。
如果这个位置上没有元素，它就可以直接存储在这个位置上，不用再进行任何比较了**；如果这个位置上**
**已经有元素了，就调用它的equals方法与新元素进行比较，相同的话就不存了，不相同就散列其它的地**
**址。**这样一来实际调用equals方法的次数就大大降低了，几乎只需要一两次。

### 6Java创建对象有几种方式？

java中提供了以下四种创建对象的方式:

1. **new**创建新对象
2. 通过**反射**机制
3. 采用**clone**机制
4. 通过**序列化**机制

### 7有没有可能两个不相等的对象有相同的hashcode

有可能.在产生hash冲突时,两个不相等的对象就会有相同的 hashcode 值.当hash冲突产生时,一般有以
下几种方式来处理:

1. **拉链法**:每个哈希表节点都有一个next指针,多个哈希表节点可以用next指针构成一个单向链表，被
   分配到同一个索引上的多个节点可以用这个单向链表进行存储.
2. **开放定址法**:一旦发生了冲突,就去寻找下一个空的散列地址,只要散列表足够大,空的散列地址总能找
   到,并将记录存入
3. **再哈希**:又叫双哈希法,有多个不同的Hash函数.当发生冲突时,使用第二个,第三个….等哈希函数计算
   地址,直到无冲突.

### 8拷贝和浅拷贝的区别是什么?

**浅拷贝**:

​		被复制对象的所有变量都含有与原来的对象相同的值,而所有的对其他对象的引用仍然指向原来的对象.
​	换言之,**浅拷贝仅仅复制所考虑的对象,而不复制它所引用的对象.**
**深拷贝:**
​		被复制对象的所有变量都含有与原来的对象相同的值.而那些引用其他对象的变量将指向被复制过的新对
​	象.而不再是原有的那些被引用的对象.换言之.**深拷贝把要复制的对象所引用的对象都复制了一遍.**

### 9static都有哪些用法?

**静态变量**和**静态方法**.也就是被static所修饰的变量/方法
都属于类的静态资源,**类实例所共享**.
除了静态变量和静态方法之外,static也用于**静态块**,**多用于初始化操作**

最后一种用法就是**静态导包**,即 import static .import static是在JDK 1.5之后引入的新特性,可以用来指
定导入某个类中的静态资源,并且不需要使用类名,可以直接使用资源名

demo:

```
import static java.lang.Math.*;
```

### 10a=a+b与a+=b有什么区别吗?

+= 操作符会进行**隐式自动类型转换**,此处a+=b隐式的将加操作的结果类型强制转换为持有结果的类型,
而a=a+b则**不会自动进行类型转换**.

+=操作符会对右边的表达式结果**强转匹配左边**的数据类型

### 11final、finalize()、finally

**性质不同**

1. final为关键字；

2. **finalize()为方法**；

3. finally为区块标志，用于try语句中；
   作用

4. final为用于**标识常量的关键字**，final标识的关键字存储在**常量池**中

5. finalize()方法**在Object中进行了定义**，用于在对象“消失”时，**由JVM进行调用用于对对象进行垃圾**
   **回收**，类似于C++中的析构函数；用户自定义时，用于释放对象占用的资源（比如进行I/0操作）；

6. finally{}用于标识代码块，与try{}进行配合，不论try中的代码执行完或没有执行完（这里指有异
   常），该代码块之中的程序必定会进行；

7. **Java 中的 final 关键字用法**
   (1)修饰类：表示该类不能被继承；
     (2)修饰方法：表示方法不能被重写；
     (3)修饰变量：表示变量只能一次赋值以后值不能被修改（常量）。

8. ### 12JDBC操作的步骤

  加载数据库驱动类 打开数据库连接 执行sql语句 处理返回结果 关闭资源

### 13在使用jdbc的时候，如何防止出现sql注入的问题。

使用**PreparedStatement**类，而不是使用Statement类

### 14连接池，使用连接池有什么好处？

数据库连接是非常消耗资源的，影响到程序的性能指标。**连接池是用来分配、管理、释放数据库连接**
**的**，可以使应用程序重复使用同一个数据库连接，而不是每次都创建一个新的数据库连接。通过释放空
闲时间较长的数据库连接避免数据库因为创建太多的连接而造成的连接遗漏问题，提高了程序性能

Spring 推荐使用dbcp；
Hibernate 推荐使用**c3p0**和proxool

还有阿里巴巴的**Druid**也很不错

### 15&和&&的区别

**&是位运算符**。**&&是布尔逻辑运算符**，在进行逻辑判断时用**&处理的前面为false后面的内容仍需处理**，
**用&&处理的前面为false不再处理后面的内容**
