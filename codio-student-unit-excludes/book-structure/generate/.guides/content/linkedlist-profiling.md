For the next exercise I provide a class called `Profiler` that contains code that runs a method with a range of problem sizes, measures runtimes, and plots the results.


You will use `Profiler` to classify the performance of the `add` method for the Java implementations of `ArrayList` and `LinkedList`.

Here's an example that shows how to use the profiler:

```code
    public static void profileArrayListAddEnd() {
        Timeable timeable = new Timeable() {
            List<String> list;

            public void setup(int n) {
                list = new ArrayList<String>();
            }

            public void timeMe(int n) {
                for (int i=0; i<n; i++) {
                    list.add("a string");
                }
            }
        };

        String title = "ArrayList add end";
        Profiler profiler = new Profiler(title, timeable);

        int startN = 4000;
        int endMillis = 1000;
        XYSeries series = profiler.timingLoop(startN, endMillis);
        profiler.plotResults(series);
    }
```

This method measures the time it takes to run `add` on an `ArrayList`, which adds the new element at the end. I'll explain the code and then show the results.


In order to use `Profiler`, we need to create a `Timeable` object that provides two methods: `setup` and `timeMe`. The `setup` method does whatever needs to be done before we start the clock; in this case it creates an empty list. Then `timeMe` does whatever operation we are trying to measure; in this case it adds $n$ elements to the list.


The code that creates `timeable` is an **anonymous class** that defines a new implementation of the `Timeable` interface and creates an instance of the new class at the same time. If you are not familiar with anonymous classes, you can read about them here: [http://thinkdast.com/anonclass](http://thinkdast.com/anonclass).

But you don't need to know much for the next exercise; even if you are not comfortable with anonymous classes, you can copy and modify the example code.

The next step is to create the `Profiler` object, passing the `Timeable` object and a title as parameters.

The `Profiler` provides `timingLoop` which uses the `Timeable` object stored as an instance variable. It invokes the `timeMe` method on the `Timeable` object several times with a range of values of $n$. `timingLoop` takes two parameters:



* 
`startN` is the value of $n$ the timing loop should
start at.

* 
`endMillis` is a threshold in milliseconds. As
`timingLoop` increases the problem size, the runtime increases;
when the runtime exceeds this threshold, `timingLoop` stops.


When you run the experiments, you might have to adjust these parameters. If `startN` is too low, the runtime might be too short to measure accurately. If `endMillis` is too low, you might not get enough data to see a clear relationship between problem size and runtime.

This code is in `ProfileListAdd.java`, which you'll run in the next exercise. When I ran it, I got this output:

```code
4000, 3
8000, 0
16000, 1
32000, 2
64000, 3
128000, 6
256000, 18
512000, 30
1024000, 88
2048000, 185
4096000, 242
8192000, 544
16384000, 1325
```

The first column is problem size, $n$; the second column is runtime in milliseconds. The first few measurements are pretty noisy; it might have been better to set `startN` around 64000.


The result from `timingLoop` is an `XYSeries` that contains this data. If you pass this series to `plotResults`, it generates a plot like the one in Figure 4.1.

![Figure 4.1 \caption{Profiling results: runtime versus problem size for](figs/profile1.png)

**Figure 4.1 \caption{Profiling results: runtime versus problem size for**

The next section explains how to interpret it.