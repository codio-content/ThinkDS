Before we go on, we should check whether `MyHashMap.put` is really constant time.

{Run! | terminal}(cd code && javac Profiler.java ProfileMapPut.java && java -cp lib/*:. ProfileMapPut && cd ../ )

It measures the runtime of `HashMap.put` (provided by Java) with a range of problem sizes, and plots runtime versus problem size on a log-log scale. If this operation is constant time, the total time for $n$ operations should be linear, so the result should be a straight line with slope 1. When I ran this code, the estimated slope was close to 1, which is consistent with our analysis. You should get something similar. 



Modify `ProfileMapPut.java` so it profiles your implementation, `MyHashMap`, instead of Java's `HashMap`. Run the profiler again and see if the slope is near 1. You might have to adjust `startN` and `endMillis` to find a range of problem sizes where the runtimes are more than a few milliseconds, but not more than a few thousand.

When I ran this code, I got a surprise: the slope was about 1.7, which suggests that this implementation is not constant time after all. It contains a “performance bug”. 


Before you read the next section, you should track down the error, fix it, and confirm that `put` is now constant time, as expected.