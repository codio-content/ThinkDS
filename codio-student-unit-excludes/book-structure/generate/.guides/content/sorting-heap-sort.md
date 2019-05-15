In addition to radix sort, which applies when the things you want to sort are bounded in size, there is one other special-purpose sorting algorithm you might encounter: bounded heap sort. Bounded heap sort is useful if you are working with a very large dataset and you want to report the “Top 10” or “Top k” for some value of $k$ much smaller than $n$.

For example, suppose you are monitoring a Web service that handles a billion transactions per day. At the end of each day, you want to report the $k$ biggest transactions (or slowest, or any other superlative). One option is to store all transactions, sort them at the end of the day, and select the top $k$. That would take time proportional to $n \log n$, and it would be very slow because we probably can't fit a billion transactions in the memory of a single program. We would have to use an “out of core” sort algorithm. You can read about external sorting at [http://thinkdast.com/extsort](http://thinkdast.com/extsort).


Using a bounded heap, we can do much better! Here's how we will proceed:



1. 
I'll explain (unbounded) heap sort.

1. 
You'll implement it.

1. 
I'll explain bounded heap sort and analyze it.



To understand heap sort, you have to understand a heap, which is a data structure similar to a binary search tree (BST). Here are the differences:



* 
In a BST, every node, `x`, has the “BST property”: all nodes
in the left subtree of `x` are less than `x` and all
nodes in the right subtree are greater than `x`.

* 
In a heap, every node, `x`, has the “heap property”: all
nodes in both subtrees of `x` are greater than `x`.

* 
Heaps are like balanced BSTs; when you add or remove elements, they
do some extra work to rebalance the tree.  As a result, they can
be implemented efficiently using an array of elements.


The smallest element in a heap is always at the root, so we can find it in constant time. Adding and removing elements from a heap takes time proportional to the height of the tree $h$. And because the heap is always balanced, $h$ is proportional to $\log n$.  You can read more about heaps at [http://thinkdast.com/heap](http://thinkdast.com/heap).


The Java `PriorityQueue` is implemented using a heap. `PriorityQueue` provides the methods specified in the `Queue` interface, including `offer` and `poll`:



* 
`offer`: Adds an element to the queue, updating the heap so
that every node has the “heap property”. Takes $\log n$ time.

* 
`poll`: Removes the smallest element in the queue from the root
and updates the heap. Takes $\log n$ time.


Given a `PriorityQueue`, you can easily sort of a collection of $n$ elements like this:



1. 
Add all elements of the collection to a `PriorityQueue` using
`offer`.

1. 
Remove the elements from the queue using `poll` and add them to
a `List`.


Because `poll` returns the smallest element remaining in the queue, the elements are added to the `List` in ascending order. This way of sorting is called **heap sort** (see [http://thinkdast.com/heapsort](http://thinkdast.com/heapsort)).


Adding $n$ elements to the queue takes $n \log n$ time. So does removing $n$ elements. So the runtime for heap sort is $O(n \log n)$.


In the repository for this book, in `ListSorter.java` you'll find the outline of a method called `heapSort`. Fill it in and then run `ant ListSorterTest` to confirm that it works.