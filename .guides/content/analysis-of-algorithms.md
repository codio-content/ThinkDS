As we saw in the previous chapter, Java provides two implementations of the `List` interface, `ArrayList` and `LinkedList`. For some applications `LinkedList` is faster; for other applications `ArrayList` is faster.


To decide which one is better for a particular application, one approach is to try them both and see how long they take. This approach, which is called “profiling”, has a few problems:



1.  Before you can compare the algorithms, you have to implement them both.
1.  The results might depend on what kind of computer you use. One algorithm might be better on one machine; the other might be better on a different machine.
1.  The results might depend on the size of the problem or the data provided as input. 

We can address some of these problems using **analysis of   algorithms**. When it works, algorithm analysis makes it possible to compare algorithms without having to implement them. But we have to make some assumptions:



1.  To avoid dealing with the details of computer hardware, we usually identify the basic operations that make up an algorithm --- like addition, multiplication, and comparison of numbers --- and count the number of operations each algorithm requires.
1.  To avoid dealing with the details of the input data, the best option is to analyze the average performance for the inputs we expect. If that's not possible, a common alternative is to analyze the worst case scenario.
1.  Finally, we have to deal with the possibility that one algorithm works best for small problems and another for big ones. In that case, we usually focus on the big ones, because for small problems the difference probably doesn't matter, but for big problems the difference can be huge. 

This kind of analysis lends itself to simple classification of algorithms. For example, if we know that the runtime of Algorithm A tends to be proportional to the size of the input, $n$, and Algorithm B tends to be proportional to $n^2$, we expect A to be faster than B, at least for large values of $n$.


Most simple algorithms fall into just a few categories.



*  Constant time: An algorithm is “constant time” if the runtime does not depend on the size of the input. For example, if you have an array of $n$ elements and you use the bracket operator (`[]`) to access one of the elements, this operation takes the same number of operations regardless of how big the array is.
*  Linear: An algorithm is “linear” if the runtime is proportional to the size of the input. For example, if you add up the elements of an array, you have to access $n$ elements and perform $n-1$ additions. The total number of operations (element accesses and additions) is $2n-1$, which is proportional to $n$.
*  Quadratic: An algorithm is “quadratic” if the runtime is proportional to $n^2$.  For example, suppose you want to check whether any element in a list appears more than once.  A simple algorithm is to compare each element to all of the others.  If there are $n$ elements and each is compared to $n-1$ others, the total number of comparisons is $n^2 -n$, which is proportional to $n^2$ as $n$ grows.