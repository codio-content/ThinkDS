In the previous exercise you also profiled the performance of adding new elements at the beginning of a `LinkedList`. Based on our analysis, we expect each `add` to take constant time, because in a linked list, we don't have to shift the existing elements; we can just add a new node at the beginning. So we expect the total time for $n$ adds to be linear.


Here's a solution:

\begin{verbatim}
    public static void profileLinkedListAddBeginning() {
        Timeable timeable = new Timeable() {
            List<String> list;

            public void setup(int n) {
                list = new LinkedList<String>();
            }

            public void timeMe(int n) {
                for (int i=0; i<n; i++) {
                    list.add(0, "a string");
                }
            }
        };
        int startN = 128000;
        int endMillis = 2000;
        runProfiler("LinkedList add beginning", timeable, startN, endMillis);
    }
\end{verbatim}

We only had a make a few changes, replacing `ArrayList` with `LinkedList` and adjusting `startN` and `endMillis` to get a good range of data. The measurements were noisier than the previous batch; here are the results:

\begin{verbatim}
128000, 16
256000, 19
512000, 28
1024000, 77
2048000, 330
4096000, 892
8192000, 1047
16384000, 4755
\end{verbatim}

Figure 6.2 shows the graph of these results.

![Figure 6.2 \caption{Profiling results: runtime versus problem size for adding](figs/profile3.png)

**Figure 6.2 \caption{Profiling results: runtime versus problem size for adding**

It's not a very straight line, and the slope is not exactly 1; the slope of the least squares fit is 1.23. But these results indicate that the total time for $n$ adds is at least approximately $O(n)$, so each add is constant time.