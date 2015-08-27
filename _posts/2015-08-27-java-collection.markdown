
---
layout: post
title: "Java集合类简单总结"
date: 2015-08-27 19:28
comments: true
categories: work
tags: [java]
---
一、java.util.Map，四个实现类分别是HashMap、HashTable、LinkedHashMap和TreeMap。

| HashMap| HashTable | LinkedHashMap |WeakHashMap |IdentityHashMap|TreeMap|
| ------------ | ------------- | ------------ |------------ |------------ |------------ |
| HashMap是一个最常用的Map，它根据键的hashCode值存储数据，根据键可以直接获取它的值，具有很快的访问速度。HashMap最多只允许一条记录的键为null，不允许多条记录的值为null。HashMap不支持线程的同步，即任一时刻可以有多个线程同时写HashMap，可能会导致数据的不一致。如果需要同步，可以用Collections.synchronizedMap(HashMap map)方法使HashMap具有同步的能力。 | Hashtable与HashMap类似，不同的是：它不允许记录的键或者值为空；它支持线程的同步，即任一时刻只有一个线程能写Hashtable，然而，这也导致了Hashtable在写入时会比较慢。 | LinkedHashMap保存了记录的插入顺序，在用Iteraor遍历LinkedHashMap时，先得到的记录肯定是先插入的。在遍历的时候会比HashMap慢。有HashMap的全部特性。| 在短时间内就过期的缓存时最好使用WeakHashMap.以弱键实现的基于哈希表的map。当某个键不再正常使用时，将自动移除其条目。精确来说，对于一个给定的键，其映射的存在并不阻止垃圾回收器对该键的丢弃，这就使该键成为可终止的，被终止，然后被回收的对象。 |1、比较key是否相等，比较的是引用，而不是内容，即用==而不是用equals()即：当且仅当key1 == key2 时，才认为是两个键相等。2、用一Object数组存储key-value对，数组大小为map容量的2倍，在i索引处存放key，i+1索引处存放value 3、处理冲突采用线性探测法。 |TreeMap能够把它保存的记录根据键排序，默认是按升序排序，也可以指定排序的比较器。当用Iteraor遍历TreeMap时，得到的记录是排过序的。TreeMap的键和值都不能为空。|







| HashMap      | HashTable     | Third Header |Third Header |Third Header |Third Header |
| ------------ | ------------- | ------------ |------------ |------------ |------------ |
| Content Cell | Content Cell  | Content Cell |Content Cell |Third Header |Third Header |
