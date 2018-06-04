# Collection\<E\>

## Javadoc
背包和多重集应直接实现这个接口
<br>
所有直接或间接实现该接口的类，都应提供两个构造器，无参构造器（构造空集合）和一个参数的构造器（此参数为Collection类型，构造相同元素的集合）

## Object[] toArray();
**进行保护性复制**,返回的数组是底层数组的一份副本.若没有任何顺序保证,返回顺序和iterator()方法相同

## <T> T[] toArray(T[] a);
返回T类型的数组,如String[] y = toArray(new String[0]) , Object[] y = toArray(new Object[0])和toArray()方法相等

## boolean add(E e);
如果集合发生改变则返回true,如果集合元素不允许重复且已经拥有返回false.
<br>
如果集合拒绝添加一个元素不是由于已经存在的元素,则应该抛出异常.

## 其他方法略
