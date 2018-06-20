# TreeMap\<K,V\> extends AbstractMap\<K,V\> implements NavigableMap\<K,V\>, Cloneable, Serializable

## Javadoc
- 对于subMap(K, boolean, K, boolean)(定义在NavigableMap中)方法，指定选取的范围是否要包含边界值，重载的subMap(定义在SortedMap中)是左闭右开
- 红黑树实现，containsKey, get, put, remove方法时间复杂度为logn
- 四个构造器,分别为无参构造器，一个参数(Comparator)构造器，一个参数(Map)构造器，一个参数(SortedMap,使用它的comparator)的构造器

## Fields

    private final Comparator<? super K> comparator; //使用自然排序时为null
    private transient Entry<K,V> root; //根节点
    private transient int size = 0;
    private transient int modCount = 0;
