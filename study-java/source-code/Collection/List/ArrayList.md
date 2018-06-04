# ArrayList\<E\> extends AbstractList\<E\> implements List\<E\>, RandomAccess, Cloneable, java.io.Serializable

## Javadoc
底层使用自动调整长度的数组，允许所有元素包括null，该类几乎等于Vector，除了不是同步的
<br>
*时间复杂度为常数的方法*

- size
- isEmpty
- get
- set
- iterator
- listIterator

add方法时间复杂度为O(n),其他操作都是复杂度为线性
## Fields,由于1.2时没有泛型,所以底层是Object[]

    private static final int DEFAULT_CAPACITY = 10;//默认初始化的容量
    private static final Object[] EMPTY_ELEMENTDATA = {};//空的数组对象
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};//有默认容量的空的数组对象
    transient Object[] elementData; //存储元素的数组缓冲区 non-private to simplify nested class access
    private int size;//ArrayList的size

## Methods

**Collection文档规定,需要提供无参构造器**

    //构造默认长度的ArrayList
    public ArrayList() {
       this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }
    //额外的，提供了根据指定容量的构造的构造器
    public ArrayList(int initialCapacity) {
        if (initialCapacity > 0) {
            this.elementData = new Object[initialCapacity];
        } else if (initialCapacity == 0) {
            this.elementData = EMPTY_ELEMENTDATA;
        } else {
            throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        }
    }

**Collection文档规定,需要提供有一个参数的构造器**

    public ArrayList(Collection<? extends E> c) {
        //将c中的元素转成数组后赋给elementData
        //...
    }

**其他方法**

    public void trimToSize() {
      //...  将ArrayList的长度缩短为当前size的实际长度
    }
    //指定容量大小
    public void ensureCapacity(int minCapacity) {
      int minExpand = (elementData != DEFAULTCAPACITY_EMPTY_ELEMENTDATA)
          ? 0
          : DEFAULT_CAPACITY;

      if (minCapacity > minExpand) {
          ensureExplicitCapacity(minCapacity);
      }
    }

public boolean contains(Object o)和public int indexOf(Object o)
<br>
contains方法调用indexOf方法，indexOf方法依赖于equals
