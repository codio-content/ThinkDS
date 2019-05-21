For example, see the implementation of a simple algorithm called *selection sort** (see \url{http://thinkdast.com/selectsort}) in the panel to the left.

[Highlight swapElements](open_file code/SelectionSort.java panel=0 ref="public static void swapElements" count=5)



The first method, `swapElements`, swaps two elements of the array. Reading and writing elements are constant time operations, because if we know the size of the elements and the location of the first, we can compute the location of any other element with one multiplication and one addition, and those are constant time operations. Since everything in `swapElements` is constant time, the whole method is constant time.

[Highlight indexLowest](open_file code/SelectionSort.java panel=0 ref="public static int indexLowest" count=9)


The second method, `indexLowest`, finds the index of the smallest element of the array starting at a given index, `start`. Each time through the loop, it accesses two elements of the array and performs one comparison. Since these are all constant time operations, it doesn't really matter which ones we count. To keep it simple, let's count the number of comparisons.



1.  If `start` is 0, `indexLowest` traverses the entire array, and the total number of comparisons is the length of the array, which I'll call $n$.
1.  If `start` is 1, the number of comparisons is $n-1$.
1.  In general, the number of comparisons is $n$ - `start`, so `indexLowest` is linear. 
[Highlight selectionSort](open_file code/SelectionSort.java panel=0 ref="public static void selectionSort" count=6)


The third method, `selectionSort`, sorts the array. It loops from 0 to $n-1$, so the loop executes $n$ times. Each time, it calls `indexLowest` and then performs a constant time operation, `swapElements`.


The first time `indexLowest` is called, it performs $n$ comparisons. The second time, it performs $n-1$ comparisons, and so on. The total number of comparisons is

$ n + n-1 + n-2 + ... + 1 + 0 $

The sum of this series is $n(n+1)/2$, which is proportional to $n^2$; and that means that `selectionSort` is quadratic.


To get to the same result a different way, we can think of `indexLowest` as a nested loop. Each time we call `indexLowest`, the number of operations is proportional to $n$. We call it $n$ times, so the total number of operations is proportional to $n^2$.