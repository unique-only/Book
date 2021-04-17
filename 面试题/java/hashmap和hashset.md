参考地址：https://blog.csdn.net/weixin_34254823/article/details/94558911?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control



### 概述

hashmap概述:基于map接口实现，键值对都允许为空，但是key不可重复，值可重复。而且她不能保证放入元素的顺序，线程不安全。如果你想要在多线程下使用hashmap，需要使用Collections.synchronized方法来获取一个线程安全的集合

实现：

```java
public class HashMap<K,V> 
    extends AbstractMap<K,V>
    implements Map<K,V>, Cloneable, Serializable {
}
```



hashtable概述：他是线程安全的，因为实现的方法里面都用了synchronized关键字来保证线程安全。同时他不允许键值对为空，键不可重复，值可重复。

实现：

```java
public class Hashtable<K,V>
    extends Dictionary<K,V>
    implements Map<K,V>, Cloneable, java.io.Serializable {
}
```



### 初始容量以及扩容

HashMap的初始容量为16，Hashtable的初始容量为11。

HashMap扩容机制是当前容量翻倍，Hashtable扩容是当前容量*2+1

两者的装填因子都是0.75.

作用：装填因子是根据线性探测法过来的，=关键字/表长。装填因子在hashmap和hashtable中的作用就是当表中关键字超过  （hashmap为例）0.75*16=12时，他会触发扩容机制





首先hashmap是由链表和数组组成的，当使用put的时候，先进行一个扩容判断，然后会对插入的key值进行hashcode计算，得到相应的数组下标，如果这个数组后面的链表没有元素，那就直接插入进来，如果有元素，就需要用equals进行对比，如果都不相同，就直接插入尾端，如果有元素相同，就说明这个key的地址是相同的，那么直接对这个数据进行覆盖。在jdk1.8之后，就引入了红黑树，就是当链表结构的长度超过8，就自动转换为红黑树，他其实就是一个平衡排序二叉树，这样在进行数据查找的时候大大增加了速度







hashset的底层实现：

首先hashset是基于hashmap底层来实现的，他使用add都是放到key中，它允许key为null，但不允许重复。