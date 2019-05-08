Adding elements at the beginning is one of the operations where we expect `LinkedList` to be faster than `ArrayList`. But for adding elements at the end, we expect `LinkedList` to be slower. In my implementation, we have to traverse the entire list to add an element to the end, which is linear. So we expect the total time for $n$ adds to be quadratic.


Well, it's not.  Here's the code:

\begin{verbatim}
    public static void profileLinkedListAddEnd() {
        Timeable timeable = new Timeable() {
            List<String> list;

            public void setup(int n) {
                list = new LinkedList<String>();
            }

            public void timeMe(int n) {
                for (int i=0; i<n; i++) {
                    list.add("a string");
                }
            }
        };
        int startN = 64000;
        int endMillis = 1000;
        runProfiler("LinkedList add end", timeable, startN, endMillis);
    }
\end{verbatim}

Here are the results:

\begin{verbatim}
64000, 9
128000, 9
256000, 21
512000, 24
1024000, 78
2048000, 235
4096000, 851
8192000, 950
16384000, 6160
\end{verbatim}

Figure 6.3 shows the graph of these results.

![Figure 6.3 \caption{Profiling results: runtime versus problem size for adding](figs/profile4.png)

**Figure 6.3 \caption{Profiling results: runtime versus problem size for adding**


Again, the measurements are noisy and the line is not perfectly straight, but the estimated slope is 1.19, which is close to what we got adding elements at the beginning, and not very close to 2, which is what we expected based on our analysis. In fact, it is closer to 1, which suggests that adding elements at the end is constant time. What's going on?