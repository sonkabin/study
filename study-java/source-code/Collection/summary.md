## ArrayList

1. 容量默认为10,能自动扩容，每次增加当前长度的一半，扩容使用Arrays.copyOf
2. 数组容量达到Integer.MAX_VALUE-8时，会限制数组扩容，超过Integer.MAX_VALUE会抛出内存溢出异常
3. 允许所有元素
4. 线程不安全
5. 迭代器初始化时，用modCount初始化expectedModCount,在迭代器的操作中要检查这两个值的等值性，如果不相等抛出ConcurrentModificationException异常，表示当前list正在被修改，为什么呢？原因如下：
<br>
List的add/remove方法会修改modCount值，如果在迭代器操作过程中调用List本身的add/remove方法就会导致modCount和expectedModCount不相等，而调用迭代器自身的remove方法不会有这个问题，因为它会在remove方法调用完成后更新expectedModCount为modCount的值
6. ListIterator和普通的迭代器类似，只是多了双向迭代的功能
7. 通过subList方法得到的list，对它进行修改会改变原来的list
8. ArrayList的sort方法是调用Arrays.sort传入比较器实现的
9. clone是浅拷贝，拷贝出的对象指向相同的数据

## LinkedList

1. 不需要扩容，只需要处理好指针引用的指向关系
2. 内部维护size，指针first和last，支持双向遍历
3. 允许所有元素
4. 线程不安全
5. 支持表头增删，表尾增删,指定节点前后增删
6. Node为静态私有内部类
7. LinkedList的迭代器只有ListIterator,也有expectedModCount检测修改状态
8. clone是浅拷贝
9. 同时实现了Deque，导致它变成了宽接口，感觉并不是好的设计
10. 一个有用的包级方法Node<E> node(int index)，也就是遍历寻找特定索引的Node，做了优化，若小于一半的长度，则从前往后找，否则从后往前找

### ArrayList和LinkedList的优缺点
- ArrayList随机访问效率高，在尾部插入和删除的效率能接受(考虑扩容)，但中间插入和删除的效率低．要求有连续的空间
- LinkedList插入和删除效率高，但随机访问效率低，可以使用分散的空间
