# public class LinkedHashMap\<K,V\> extends HashMap\<K,V\> implements Map\<K,V\>

## Javadoc
- 所有的entry维护一个双向链表，定义了迭代的顺序(即key插入的顺序)，key重复插入不会影响顺序
- 有一个特别的构造器适合提供LRU缓存,

      public LinkedHashMap(int initialCapacity, float loadFactor, boolean accessOrder) // 对于迭代器的顺序，accessOrder为true时，将使用访问顺序(LRU)，为false时，和其他的构造器效果相同，按插入顺序

- 允许键和值为null
- 常数时间的操作有add, remove, contains, 只要hash函数很优秀
- 性能和HashMap比稍差，但是遍历比HashMap快，由于LinkedHashMap需要的时间和size成比例，而HashMap需要的时间和capacity成比例
- 影响性能的两个参数和HashMap相同，即capacity和load factor，值得注意的是，**为初始容量选择过高的值的代价小于HashMap(迭代时间不受容量影响)**
- 不是线程安全的
- 使用迭代器和List一样，注意ConcurrentModificationException异常

## Fields
除了HashMap中的外，还有

    transient LinkedHashMap.Entry<K,V> head;
    transient LinkedHashMap.Entry<K,V> tail;
    final boolean accessOrder;

## Methods

    //在put和putAll方法插入entry后，被他们调用，当map代表的是cache时，很有用，它可以让map删除旧的元素来减少内存的消耗，返回true时表示需要移除最旧的元素，返回false则和正常的map表现一致，**注意，它默认是返回false的，因此想用LinkedHashMap作缓存的话，需要继承此类重写这个方法**
    protected boolean removeEldestEntry(Map.Entry<K,V> eldest) {
        return false;
    }
    //如下是一个例子,维护100个entry
    private static final int MAX_ENTRIES = 100;
    protected boolean removeEldestEntry(Map.Entry eldest) {
       return size() > MAX_ENTRIES;
    }
<br>

**钩子方法afterNodeAccess**，主要用来将访问过的entry放到链表尾部，当accessOrder为true时，get和put方法都会调用此方法
