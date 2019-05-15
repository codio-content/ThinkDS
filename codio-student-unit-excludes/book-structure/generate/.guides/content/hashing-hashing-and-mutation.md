`String`s are immutable, and `SillyString` is also immutable because `innerString` is declared to be `final`. Once you create a `SillyString`, you can't make `innerString` refer to a different `String`, and you can't modify the `String` it refers to. Therefore, it will always have the same hash code.


But let's see what happens with a mutable object. Here's a definition for `SillyArray`, which is identical to `SillyString`, except that it uses an array of characters instead of a `String`:

```code
public class SillyArray {
    private final char[] array;

    public SillyArray(char[] array) {
        this.array = array;
    }

    public String toString() {
        return Arrays.toString(array);
    }
    
    @Override
    public boolean equals(Object other) {
        return this.toString().equals(other.toString());
    }
    
    @Override
    public int hashCode() {
        int total = 0;
        for (int i=0; i<array.length; i++) {
            total += array[i];
        }
        System.out.println(total);
        return total;
    }
```


`SillyArray` also provides `setChar`, which makes it possible to modify the characters in the array:

```code
public void setChar(int i, char c) {
    this.array[i] = c;
}
```

Now suppose we create a `SillyArray` and add it to a map:

```code
SillyArray array1 = new SillyArray("Word1".toCharArray());
map.put(array1, 1);
```

The hash code for this array is 461. Now if we modify the contents of the array and then try to look it up, like this:

```code
array1.setChar(0, 'C');
Integer value = map.get(array1);
```

the hash code after the mutation is 441. With a different hash code, there's a good chance we'll go looking in the wrong sub-map. In that case, we won't find the key, even though it is in the map. And that's bad.


In general, it is dangerous to use mutable objects as keys in data structures that use hashing, which includes `MyBetterMap` and `HashMap`. If you can guarantee that the keys won't be modified while they are in the map, or that any changes won't affect the hash code, it might be OK. But it is probably a good idea to avoid it.