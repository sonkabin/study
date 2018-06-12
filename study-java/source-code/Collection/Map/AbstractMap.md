# AbstractMap\<K,V\> implements Map\<K,V\>

## Javadoc
实现不可修改的map：实现entrySet方法，返回的set不允许支持add和remove方法，同时该set的迭代器也不允许支持remove方法
<br>
实现可修改的map：实现put，entrySet().iterator()支持remove方法
<br>
和Collection相同的是，实现类约定要提供无参构造器和一个接受map参数的构造器

## keySet和values被调用时只创建一次
单例，没有使用synchronized
## 有两个静态公有内部类SimpleEntry和SimpleImmutableEntry
SimpleEntry的value可以修改(调用setValue方法)，SimpleImmutableEntry的value不可以修改(setValue方法抛异常)
