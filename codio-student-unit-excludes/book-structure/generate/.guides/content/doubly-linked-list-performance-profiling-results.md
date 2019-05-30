In the previous exercise, we used `Profiler.java` to run various `ArrayList` and `LinkedList` operations with a range of problem sizes. We plotted runtime versus problem size on a log-log scale and estimated the slope of the resulting curve, which indicates the leading exponent of the relationship between runtime and problem size.


For example, when we used the `add` method to add elements to the end of an `ArrayList`, we found that the total time to perform $n$ adds was proportional to $n$; that is, the estimated slope was close to 1. We concluded that performing $n$ adds is in $O(n)$, so on average the time for a single add is constant time, or $O(1)$, which is what we expect based on algorithm analysis.



The exercise asks you to fill in the body of `profileArrayListAddBeginning`, which tests the performance of adding new elements at the beginning of an `ArrayList`. Based on our analysis, we expect each add to be linear, because it has to shift the other elements to the right; so we expect $n$ adds to be quadratic.


Here's a solution, which you can find in the `solution` directory of the repository.

```code
    public static void profileArrayListAddBeginning() {
        Timeable timeable = new Timeable() {
            List<String> list;

            public void setup(int n) {
                list = new ArrayList<String>();
            }

            public void timeMe(int n) {
                for (int i=0; i<n; i++) {
                    list.add(0, "a string");
                }
            }
        };
        int startN = 4000;
        int endMillis = 10000;
        runProfiler("ArrayList add beginning", timeable, startN, endMillis);
    }
```

This method is almost identical to `profileArrayListAddEnd`. The only difference is in `timeMe`, which uses the two-parameter version of `add` to put the new element at index 0. Also, we increased `endMillis` to get one additional data point.

Here are the timing results (problem size on the left, runtime in milliseconds on the right):

```code
4000, 14
8000, 35
16000, 150
32000, 604
64000, 2518
128000, 11555
```

Figure 5.1 shows the graph of runtime versus problem size.

![Figure 5.1 Profiling results: runtime versus problem size for adding $n$ elements at the beginning of an `ArrayList`.](figs/profile2.png)

**Figure 5.1 Profiling results: runtime versus problem size for adding $n$ elements at the beginning of an `ArrayList`.**

Remember that a straight line on this graph does **not** mean that the algorithm is linear. Rather, if the runtime is proportional to $n^k$ for any exponent, $k$, we expect to see a straight line with slope $k$. In this case, we expect the total time for $n$ adds to be proportional to $n^2$, so we expect a straight line with slope 2. In fact, the estimated slope is 1.992, which is so close I would be afraid to fake data this good.