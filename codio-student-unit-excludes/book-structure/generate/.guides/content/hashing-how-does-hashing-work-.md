The fundamental requirement for a hash function is that the same object should produce the same hash code every time. For immutable objects, that's relatively easy. For objects with mutable state, we have to think harder.


As an example of an immutable object, I'll define a class called `SillyString` that encapsulates a `String`:

```code
public class SillyString {
    private final String innerString;

    public SillyString(String innerString) {
        this.innerString = innerString;
    }

    public String toString() {
        return innerString;
    }
```

This class is not very useful, which is why it's called `SillyString`, but I'll use it to show how a class can define its own hash function:

```code
    @Override
    public boolean equals(Object other) {
        return this.toString().equals(other.toString());
    }
    
    @Override
    public int hashCode() {
        int total = 0;
        for (int i=0; i<innerString.length(); i++) {
            total += innerString.charAt(i);
        }
        return total;
    }
```

Notice that `SillyString` overrides both `equals` and `hashCode`. This is important. In order to work properly, `equals` has to be consistent with `hashCode`, which means that if two objects are considered equal --- that is, `equals` returns `true` --- they should have the same hash code. But this requirement only works one way; if two objects have the same hash code, they don't necessarily have to be equal.


`equals` works by invoking `toString`, which returns `innerString`. So two `SillyString` objects are equal if their `innerString` instance variables are equal.


`hashCode` works by iterating through the characters in the `String` and adding them up. When you add a character to an `int`, Java converts the character to an integer using its Unicode code point. You don't need to know anything about Unicode to understand this example, but if you are curious, you can read more at  [http://thinkdast.com/codepoint](http://thinkdast.com/codepoint).


This hash function satisfies the requirement: if two `SillyString` objects contain embedded strings that are equal, they will get the same hash code.

This works correctly, but it might not yield good performance, because it returns the same hash code for many different strings. If two strings contain the same letters in any order, they will have the same hash code. And even if they don't contain the same letters, they might yield the same total, like `"ac"` and `"bb"`.

If many objects have the same hash code, they end up in the same sub-map.  If some sub-maps have more entries than others, the speedup when we have $k$ maps might be much less than $k$. So one of the goals of a hash function is to be uniform; that is, it should be equally likely to produce any value in the range.  You can read more about designing good hash functions at [http://thinkdast.com/hash](http://thinkdast.com/hash).