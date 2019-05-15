To classify the runtime of merge sort, it helps to think in terms of levels of recursion and how much work is done on each level. Suppose we start with a list that contains $n$ elements. Here are the steps of the algorithm:



1. 
Make two new arrays and copy half of the elements into each.

1. 
Sort the two halves.

1. 
Merge the halves.


Figure 17.1 shows these steps.

![Figure 17.1 Representation of merge sort showing one level of recursion.](figs/merge_sort1.jpg)

**Figure 17.1 Representation of merge sort showing one level of recursion.**


The first step copies each of the elements once, so it is linear. The third step also copies each element once, so it is also linear. Now we need to figure out the complexity of step 2. To do that, it helps to looks at a different picture of the computation, which shows the levels of recursion, as in Figure 17.2.

![Figure 17.2 Representation of merge sort showing all levels of recursion.](figs/merge_sort2.jpg)

**Figure 17.2 Representation of merge sort showing all levels of recursion.**

At the top level, we have $1$ list with $n$ elements.  For simplicity, let's assume $n$ is a power of 2. At the next level there are $2$ lists with $n/2$ elements. Then $4$ lists with $n/4$ elements, and so on until we get to $n$ lists with $1$ element.

On every level we have a total of $n$ elements. On the way down, we have to split the arrays in half, which takes time proportional to $n$ on every level. On the way back up, we have to merge a total of $n$ elements, which is also linear.

If the number of levels is $h$, the total amount of work for the algorithm is $O(nh)$. So how many levels are there? There are two ways to think about that:



1. 
How many times do we have to cut $n$ in half to get to 1?

1. 
Or, how many times do we have to double $1$ before we get to $n$?


Another way to ask the second question is “What power of 2 is $n$?”

$2^h = n$

Taking the $\log_2$ of both sides yields

$h = \log_2 n$

So the total time is $O(n \log n)$. I didn't bother to write the base of the logarithm because logarithms with different bases differ by a constant factor, so all logarithms are in the same order of growth.


Algorithms in $O(n \log n)$ are sometimes called “linearithmic”, but most people just say “n log n”.


It turns out that $O(n \log n)$ is the theoretical lower bound for sort algorithms that work by comparing elements to each other. That means there is no “comparison sort” whose order of growth is better than $n \log n$.  See [http://thinkdast.com/compsort](http://thinkdast.com/compsort).

But as we'll see in the next section, there are non-comparison sorts that take linear time!