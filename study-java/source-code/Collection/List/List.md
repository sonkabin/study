# List\<E\> extends Collection\<E\>

## boolean remove(Object o) & E remove(int index)

## int indexOf(Object o) & int lastIndexOf(Object o)
第一个出现和最后一个出现的元素

## ListIterator<E> listIterator() & ListIterator<E> listIterator(int index)
所有元素的interator和从某个位置开始的所有元素的iterator

## List<E> subList(int fromIndex, int toIndex)
**返回一个由原列表支持的列表**，两者之间改变其一对另一个有影响
<br>
包括fromIndex，不包括toIndex，所以fromIndex等于toIndex时，返回空列表
