A Java `interface` specifies a set of methods; any class that implements this `interface` has to provide these methods. For example, here is the source code for `Comparable`, which is an `interface` defined in the package `java.lang`:


```code
public interface Comparable<T> {
    public int compareTo(T o);
}
```


This `interface` definition uses a type parameter, `T`, which makes `Comparable` a **generic type**.   In order to implement this `interface`, a class has to



*  Specify the type `T` refers to, and
*  Provide a method named `compareTo` that takes an object as a parameter and returns an `int`. 


For example, here's the source code for `java.lang.Integer`:

```code
public final class Integer extends Number implements Comparable<Integer> {

    public int compareTo(Integer anotherInteger) {
        int thisVal = this.value;
        int anotherVal = anotherInteger.value;
        return (thisVal<anotherVal ? -1 : (thisVal==anotherVal ? 0 : 1));
    }

    // other methods omitted
}
```

This class extends `Number`, so it inherits the methods and instance variables of `Number`; and it implements `Comparable<Integer>`, so it provides a method named `compareTo` that takes an `Integer` and returns an `int`.


When a class declares that it implements an `interface`, the compiler checks that it provides all methods defined by the `interface`.


As an aside, this implementation of `compareTo` uses the “ternary operator”, sometimes written `?:`.  If you are not familiar with it, you can read about it at [http://thinkdast.com/ternary](http://thinkdast.com/ternary).