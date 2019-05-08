All constant time algorithms belong to a set called $O(1)$. So another way to say that an algorithm is constant time is to say that it is in $O(1)$. Similarly, all linear algorithms belong to $O(n)$, and all quadratic algorithms belong to $O(n^2)$. This way of classifying algorithms is called “big O notation”.

NOTE: I am providing a casual definition of big O notation. For a more mathematical treatment, see [http://thinkdast.com/bigo](http://thinkdast.com/bigo).

This notation provides a convenient way to write general rules about how algorithms behave when we compose them. For example, if you perform a linear time algorithm followed by a constant algorithm, the total run time is linear. Using $\in$ to mean “is a member of”:

If $f \in O(n)$ and $g \in O(1)$, $f+g \in O(n)$.

If you perform two linear operations, the total is still linear:

If $f \in O(n)$ and $g \in O(n)$, $f+g \in O(n)$.

In fact, if you perform a linear operation any number of times, $k$, the total is linear, as long as $k$ is a constant that does not depend on $n$.

If $f \in O(n)$ and $k$ is a constant, $kf \in O(n)$.

But if you perform a linear operation $n$ times, the result is quadratic:

If $f \in O(n)$, $nf \in O(n^2)$.

In general, we only care about the largest exponent of $n$. So if the total number of operations is $2n + 1$, it belongs to $O(n)$. The leading constant, 2, and the additive term, 1, are not important for this kind of analysis. Similarly, $n^2 + 100n + 1000$ is in $O(n^2)$.  Don't be distracted by the big numbers!

“Order of growth” is another name for the same idea.  An order of growth is a set of algorithms whose runtimes are in the same big O category; for example, all linear algorithms belong to the same order of growth because their runtimes are in $O(n)$.


In this context, an “order” is a group, like the *Order of the Knights of the Round Table*, which is a group of knights, not a way of lining them up. So you can imagine the *Order of Linear Algorithms* as a set of brave, chivalrous, and particularly efficient algorithms.