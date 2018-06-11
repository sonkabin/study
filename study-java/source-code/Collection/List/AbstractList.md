# AbstractList\<E\> extends AbstractCollection\<E\> implements List\<E\>

## Javadoc
如果底层是数组，实现这个抽象类；若底层是链表，实现AbstractSequentialList类
<br>
要实现不可修改的list,只需要实现get(int)和size()方法
<br>
要实现可修改的list,还需要实现set(int,E),如果list长度可变，则还需实现add(int,E)和remove(int)方法
<br>
不需要提供iterator实现，因为iterator和list iterator已经被实现了
<br>
**由于可以只实现不可修改的list，因此get和size方法都是abstract的，而可选的方法都是有默认实现的(即抛出UnsupportedOperationException)．
模板方法模式，get和size由子类实现，set/add/remove方法是钩子方法，但是ArrayList将许多方法都重写了，也就是说，如果要自己实现一个继承AbstractList
的类，可以减轻开发压力**

## add(E)
在list末尾添加元素,调用add(int,E)
## add(int,E)
默认抛出UnsupportedOperationException()，因此要实现可修改的list，需要实现此方法
<br>
set(int,E)和remove(int)同理

## protected transient int modCount = 0;
统计结构改变(size改变，或者其他的扰乱方式->指的是并发修改么?)的次数,如果这个值在进行操作(next,remove,previous,set,add)时不正确的改变了，会抛出ConcurrentModificationException
<br>
可以被子类使用,如果子类要使用，必须在使结构改变的方法(add(int,E)，remove(int)和其他重写此类方法)中让modCount增加１
<br>
当然，也可以不使用:)
