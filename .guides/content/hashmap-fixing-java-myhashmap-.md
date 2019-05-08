The problem with `MyHashMap` is in `size`, which is inherited from `MyBetterMap`:

\begin{verbatim}
    public int size() {
        int total = 0;
        for (MyLinearMap<K, V> map: maps) {
            total += map.size();
        }
        return total;
    }
\end{verbatim}

To add up the total size it has to iterate the sub-maps. Since we increase the number of sub-maps, $k$, as the number of entries, $n$, increases, $k$ is proportional to $n$, so `size` is linear.


And that makes `put` linear, too, because it uses `size`:

\begin{verbatim}
    public V put(K key, V value) {
        V oldValue = super.put(key, value);

        if (size() > maps.size() * FACTOR) {
            rehash();
        }
        return oldValue;
    }
\end{verbatim}

Everything we did to make `put` constant time is wasted if `size` is linear!


Fortunately, there is a simple solution, and we have seen it before: we have to keep the number of entries in an instance variable and update it whenever we call a method that changes it.


You'll find my solution in the repository for this book, in `MyFixedHashMap.java`.  Here's the beginning of the class definition:

\begin{verbatim}
public class MyFixedHashMap<K, V> extends MyHashMap<K, V> implements Map<K, V> {

    private int size = 0;

    public void clear() {
        super.clear();
        size = 0;
    }
\end{verbatim}

Rather than modify `MyHashMap`, I define a new class that extends it. It adds a new instance variable, `size`, which is initialized to zero.

Updating `clear` is straightforward; we invoke `clear` in the superclass (which clears the sub-maps), and then update `size`.


Updating `remove` and `put` is a little more difficult because when we invoke the method on the superclass, we can't tell whether the size of the sub-map changed. Here's how I worked around that:

\begin{verbatim}
    public V remove(Object key) {
        MyLinearMap<K, V> map = chooseMap(key);
        size -= map.size();
        V oldValue = map.remove(key);
        size += map.size();
        return oldValue;
    }
\end{verbatim}

`remove` uses `chooseMap` to find the right sub-map, then subtracts away the size of the sub-map. It invokes `remove` on the sub-map, which may or may not change the size of the sub-map, depending on whether it finds the key. But either way, we add the new size of the sub-map back to `size`, so the final value of `size` is correct.


The rewritten version of `put` is similar:

\begin{verbatim}
    public V put(K key, V value) {
        MyLinearMap<K, V> map = chooseMap(key);
        size -= map.size();
        V oldValue = map.put(key, value);
        size += map.size();

        if (size() > maps.size() * FACTOR) {
            size = 0;
            rehash();
        }
        return oldValue;
    }
\end{verbatim}

We have the same problem here: when we invoke `put` on the sub-map, we don't know whether it added a new entry. So we use the same solution, subtracting off the old size and then adding in the new size.


Now the implementation of the `size` method is simple:

\begin{verbatim}
    public int size() {
        return size;
    }
\end{verbatim}

And that's pretty clearly constant time.


When I profiled this solution, I found that the total time for putting $n$ keys is proportional to $n$, which means that each `put` is constant time, as it's supposed to be.