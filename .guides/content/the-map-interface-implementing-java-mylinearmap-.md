As usual, I provide starter code and you will fill in the missing methods. Here's the beginning of the `MyLinearMap` class definition:

\begin{verbatim}
public class MyLinearMap<K, V> implements Map<K, V> {

    private List<Entry> entries = new ArrayList<Entry>();
\end{verbatim}

This class uses two type parameters, `K`, which is the type of the keys, and `V`, which is the type of the values. `MyLinearMap` implements `Map`, which means it has to provide the methods in the `Map` interface.


A `MyLinearMap` object has a single instance variable, `entries`, which is an `ArrayList` of `Entry` objects. Each `Entry` contains a key-value pair. Here is the definition:

\begin{verbatim}
    public class Entry implements Map.Entry<K, V> {
        private K key;
        private V value;
        
        public Entry(K key, V value) {
            this.key = key;
            this.value = value;
        }
        
        @Override
        public K getKey() {
            return key;
        }
        @Override
        public V getValue() {
            return value;
        }
    }
\end{verbatim}

There's not much to it; an `Entry` is just a container for a key and a value. This definition is nested inside `MyLinearList`, so it uses the same type parameters, `K` and `V`.


That's all you need to do the exercise, so let's get started.