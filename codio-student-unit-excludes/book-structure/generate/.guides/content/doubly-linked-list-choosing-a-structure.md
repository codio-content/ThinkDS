The doubly-linked implementation is better than `ArrayList` for adding and removing at the beginning, and just as good as `ArrayList` for adding and removing at the end. So the only advantage of `ArrayList` is for `get` and `set`, which require linear time in a linked list, even if it is doubly-linked.


If you know that the runtime of your application depends on the time it takes to `get` and `set` elements, an `ArrayList` might be the better choice. If the runtime depends on adding and removing elements near the beginning or the end, `LinkedList` might be better.


But remember that these recommendations are based on the order of growth for large problems. There are other factors to consider:



* 
If these operations don't take up a substantial fraction of the
runtime for your application --- that is, if your applications spends
most of its time doing other things --- then your choice of a
`List` implementation won't matter very much.

* 
If the lists you are working with are not very big, you might not get
the performance you expect. For small problems, a quadratic algorithm
might be faster than a linear algorithm, or linear might be faster
than constant time. And for small problems, the difference probably
doesn't matter.

* 
Also, don't forget about space. So far we have focused on runtime, but
different implementations require different amounts of space. In an
`ArrayList`, the elements are stored side-by-side in a single
chunk of memory, so there is little wasted space, and computer
hardware is often faster with contiguous chunks. In a linked list,
each element requires a node with one or two links. The links take up
space (sometimes more than the data!), and with nodes scattered
around in memory, the hardware might be less efficient.


In summary, analysis of algorithms provides some guidance for choosing data structures, but only if



1. 
The runtime of your application is important,

1. 
The runtime of your application depends on your choice of data
structure, and

1. 
The problem size is large enough that the order of growth actually
predicts which data structure is better.


You could have a long career as a software engineer without ever finding yourself in this situation.