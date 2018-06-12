# HashMap<K,V> extends AbstractMap\<K,V\> implements Map\<K,V\>, Cloneable, Serializable

## Javadoc
该类几乎等同于Hashtable，除了它不是同步的，
**并且允许键和值为null**
<br>
不保证map的顺序，也不保证返回的顺序一直保持不变
<br>
get和put为常数时间，只要hash函数很优秀
<br>
迭代时间依赖于桶的数量乘Entry的数量，因此如果迭代性能很重要，那么初始容量不宜过大(或者负载因子不宜过小,这两者都影响桶的数量)
<br>
默认16个桶，负载因子为0.75，当当前的Entry数量除以容量超出负载因子时，将进行重新hash，桶的数量为原来的两倍
<br>
在使用迭代器的过程中，如果使用方法修改了map的结构(除了迭代器的remove)，将抛出ConcurrentModificationException异常，能修改map结构的方法有
- put
- remove

      Tree bins (i.e., bins whose elements are all TreeNodes) are
      ordered primarily by hashCode, but in the case of ties, if two
      elements are of the same "class C implements Comparable<C>",
      type then their compareTo method is used for ordering. (We
      conservatively check generic types via reflection to validate
      this -- see method comparableClassFor).  The added complexity
      of tree bins is worthwhile in providing worst-case O(log n)
      operations when keys either have distinct hashes or are
      orderable, Thus, performance degrades gracefully under
      accidental or malicious usages in which hashCode() methods
      return values that are poorly distributed, as well as those in
      which many keys share a hashCode, so long as they are also
      Comparable. (If neither of these apply, we may waste about a
      factor of two in time and space compared to taking no
      precautions. But the only known cases stem from poor user
      programming practices that are already so slow that this makes
      little difference.)
      Because TreeNodes are about twice the size of regular nodes, we
      use them only when bins contain enough nodes to warrant use
      (see TREEIFY_THRESHOLD). And when they become too small (due to
      removal or resizing) they are converted back to plain bins.  In
      usages with well-distributed user hashCodes, tree bins are
      rarely used.  Ideally, under random hashCodes, the frequency of
      nodes in bins follows a Poisson distribution
      (http://en.wikipedia.org/wiki/Poisson_distribution) with a
      parameter of about 0.5 on average for the default resizing
      threshold of 0.75, although with a large variance because of
      resizing granularity. Ignoring variance, the expected
      occurrences of list size k are (exp(-0.5) * pow(0.5, k) /
      factorial(k)). The first values are:

      0:    0.60653066
      1:    0.30326533
      2:    0.07581633
      3:    0.01263606
      4:    0.00157952
      5:    0.00015795
      6:    0.00001316
      7:    0.00000094
      8:    0.00000006
      more: less than 1 in ten million

      The root of a tree bin is normally its first node.  However,
      sometimes (currently only upon Iterator.remove), the root might
      be elsewhere, but can be recovered following parent links
      (method TreeNode.root()).

      All applicable internal methods accept a hash code as an
      argument (as normally supplied from a public method), allowing
      them to call each other without recomputing user hashCodes.
      Most internal methods also accept a "tab" argument, that is
      normally the current table, but may be a new or old one when
      resizing or converting.

      When bin lists are treeified, split, or untreeified, we keep
      them in the same relative access/traversal order (i.e., field
      Node.next) to better preserve locality, and to slightly
      simplify handling of splits and traversals that invoke
      iterator.remove. When using comparators on insertion, to keep a
      total ordering (or as close as is required here) across
      rebalancings, we compare classes and identityHashCodes as
      tie-breakers.

      The use and transitions among plain vs tree modes is
      complicated by the existence of subclass LinkedHashMap. See
      below for hook methods defined to be invoked upon insertion,
      removal and access that allow LinkedHashMap internals to
      otherwise remain independent of these mechanics. (This also
      requires that a map instance be passed to some utility methods
      that may create new nodes.)

      The concurrent-programming-like SSA-based coding style helps
      avoid aliasing errors amid all of the twisty pointer operations.
