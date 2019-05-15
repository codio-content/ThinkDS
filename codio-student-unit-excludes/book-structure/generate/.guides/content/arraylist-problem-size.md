The last example we'll consider is `removeAll`; here's the implementation in `MyArrayList`:

```code
    public boolean removeAll(Collection<?> collection) {
        boolean flag = true;
        for (Object obj: collection) {
            flag &= remove(obj);
        }
        return flag;
    }
```
[Highlight in Code](open_file code/MyArrayList.java panel=0 ref="public boolean removeAll" count=7)


Each time through the loop, `removeAll` invokes `remove`, which is linear.  So it is tempting to think that `removeAll` is quadratic.  But that's not necessarily the case.


In this method, the loop runs once for each element in `collection`. If `collection` contains $m$ elements and the list we are removing from contains $n$ elements, this method is in $O(nm)$. If the size of `collection` can be considered constant, `removeAll` is linear with respect to $n$. But if the size of the collection is proportional to $n$, `removeAll` is quadratic. For example, if `collection` always contains 100 or fewer elements, `removeAll` is linear. But if `collection` generally contains 1% of the elements in the list, `removeAll` is quadratic.


When we talk about **problem size**, we have to be careful about which size, or sizes, we are talking about. This example demonstrates a pitfall of algorithm analysis: the tempting shortcut of counting loops.  If there is one loop, the algorithm is *often* linear.  If there are two loops (one nested inside the other), the algorithm is *often* quadratic. But be careful! You have to think about how many times each loop runs. If the number of iterations is proportional to $n$ for all loops, you can get away with just counting the loops. But if, as in this example, the number of iterations is not always proportional to $n$, you have to give it more thought.