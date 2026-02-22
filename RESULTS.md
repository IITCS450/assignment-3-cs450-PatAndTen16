## Setup:
the lotterybench program runs the scheduler and keeps track of when a process finishes and its total running time. Each process had to count from 0 to 200000000


## Observed Results

### Run 1 (Standard workload)
| PID | Tickets | Finish Time (ticks) | CPU Time (rtime) |
|-----|---------|---------------------|------------------|
| 5   | 100     | 125                 | 105              |
| 6   | 50      | 178                 | 105              |
| 7   | 10      | 226                 | 105              |
| 8   | 5       | 249                 | 106              |
| 9   | 1       | 275                 | 69               |
| **Total Duration**: 341 ticks

### Run 2 (Standard workload)
| PID | Tickets | Finish Time (ticks) | CPU Time (rtime) |
|-----|---------|---------------------|------------------|
| 11  | 100     | 131                 | 103              |
| 12  | 50      | 187                 | 94               |
| 13  | 10      | 266                 | 81               |
| 14  | 5       | 318                 | 90               |
| 15  | 1       | 397                 | 108              |
| **Total Duration**: 454 ticks

### Run 3 (Standard workload)
| PID | Tickets | Finish Time (ticks) | CPU Time (rtime) |
|-----|---------|---------------------|------------------|
| 17  | 100     | 177                 | 107              |
| 18  | 50      | 274                 | 106              |
| 19  | 10      | 338                 | 107              |
| 20  | 5       | 391                 | 108              |
| 21  | 1       | 445                 | 104              |
| **Total Duration**: 504 ticks

### Run 4 (Standard workload)
| PID | Tickets | Finish Time (ticks) | CPU Time (rtime) |
|-----|---------|---------------------|------------------|
| 23  | 100     | 274                 | 104              |
| 24  | 50      | 369                 | 110              |
| 25  | 10      | 405                 | 105              |
| 26  | 5       | 413                 | 85               |
| 27  | 1       | 472                 | 40               |
| **Total Duration**: 529 ticks


### Key Observations
- As you can see, those with 100 tickets were able to finish before those with lesser ticket counts due to higher chances of being drawn. 

- We can see that all the processes had similar runtime, between 100 and 110 ticks on average, demonstrating they all had similar workloads.

- Some anamolies to note is with PID 26 and 27, with 5 and 1 ticket respectively, we see they had significantly less runtime. This may be due to measurement errors or terminating early before workload was finished.

#### **Total Duration Variation**
Total run time varies significantly:
- **Minimum**: 341 ticks
- **Maximum**: 529 ticks  
- **Range**: 188 ticks (55% variation)

This variation is expected in a probabilistic scheduler - when low-ticket processes get more CPU time early, they finish sooner, reducing total duration.


#### Short-term vs Long-term Behavior

**In these runs (short-term):**
- High variance between runs (up to 55% difference in total time)
- Individual process finish times can vary by 2×
- Ordering isn't always strictly by ticket count (Run 4 had PID 26 with 5 tickets finishing close to PID 25 with 10 tickets)

**long-term convergence:**
If we were to average hundreds of runs:
1. Average finishing would approach a ratio proportional to tickets
2. Standard deviation would decrease relative to the mean
3. Variation would shrink with √n (n = number of scheduling decisions)
