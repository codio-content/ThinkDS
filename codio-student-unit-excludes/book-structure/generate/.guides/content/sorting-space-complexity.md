Until now we have talked a lot about runtime analysis, but for many algorithms we are also concerned about space. For example, one of the drawbacks of merge sort is that it makes copies of the data. In our implementation, the total amount of space it allocates is $O(n \log n)$. With a more clever implementation, you can get the space requirement down to $O(n)$.

In contrast, insertion sort doesn't copy the data because it sorts the elements in place. It uses temporary variables to compare two elements at a time, and it uses a few other local variables. But its space use doesn't depend on $n$.

Our implementation of heap sort creates a new `PriorityQueue` to store the elements, so the space is $O(n)$; but if you are allowed to sort the list in place, you can run heap sort with $O(1)$ space.

One of the benefits of the bounded heap algorithm you just implemented is that it only needs space proportional to $k$ (the number of elements we want to keep), and $k$ is often much smaller than $n$.

Software developers tend to pay more attention to runtime than space, and for many applications, that's appropriate. But for large datasets, space can be just as important or more so. For example:



1.  If a dataset doesn't fit into the memory of one program, the run time often increases dramatically, or it might not run at all. If you choose an algorithm that needs less space, and that makes it possible to fit the computation into memory, it might run much faster. In the same vein, a program that uses less space might make better use of CPU caches and run faster (see [http://thinkdast.com/cache](http://thinkdast.com/cache)).
1.  On a server that runs many programs at the same time, if you can reduce the space needed for each program, you might be able to run more programs on the same server, which reduces hardware and energy costs. 

So those are some reasons you should know at least a little bit about the space needs of algorithms.



\backmatter \printindex


\end{document}