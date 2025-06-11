Design a hit counter which counts the number of hits received in the past `5` minutes (i.e., the past `300` seconds).

Your system should accept a `timestamp` parameter (**in seconds** granularity), and you may assume that calls are being made to the system in chronological order (i.e., `timestamp` is monotonically increasing). Several hits may arrive roughly at the same time.

Implement the `HitCounter` class:

- `HitCounter()` Initializes the object of the hit counter system.
- `void hit(int timestamp)` Records a hit that happened at `timestamp` (**in seconds**). Several hits may happen at the same `timestamp`.
- `int getHits(int timestamp)` Returns the number of hits in the past 5 minutes from `timestamp` (i.e., the past `300` seconds).

**Example 1:**

**Input**
\["HitCounter", "hit", "hit", "hit", "getHits", "hit", "getHits", "getHits"]
\[\[], \[1], \[2], \[3], \[4], \[300], \[300], \[301]]
**Output**
\[null, null, null, null, 3, null, 4, 3]

**Explanation**
HitCounter hitCounter = new HitCounter();
hitCounter.hit(1);       // hit at timestamp 1.
hitCounter.hit(2);       // hit at timestamp 2.
hitCounter.hit(3);       // hit at timestamp 3.
hitCounter.getHits(4);   // get hits at timestamp 4, return 3.
hitCounter.hit(300);     // hit at timestamp 300.
hitCounter.getHits(300); // get hits at timestamp 300, return 4.
hitCounter.getHits(301); // get hits at timestamp 301, return 3.

**Constraints:**

- `1 <= timestamp <= 2 * 109`
- All the calls are being made to the system in chronological order (i.e., `timestamp` is monotonically increasing).
- At most `300` calls will be made to `hit` and `getHits`.

**Follow up:** What if the number of hits per second could be huge? Does your design scale?

## Editorial
### Approach #1: Using Queue

**Intuition**

A key observation here is that all the timestamps that we will encounter are going to be in increasing order. Also as the timestamps' value increases we have to ignore the timestamps that occurred previously (having a difference of 300 or more with the latest timestamp). This is the case of considering the elements in the FIFO manner (First in first out) which is best solved by using the "queue" data structure.

**Algorithm**

We will add each timestamp to the queue in the `hit` method and will remove all the timestamps with difference greater than or equal to 300 from the queue inside `getHits`. The answer returned from the `getHits` method is then simply the size of the queue.

Below is the implementation of this approach.
```c++
class HitCounter {
private:
    
    queue<int> hits;
    
public:
    
    /** Initialize your data structure here. */
    HitCounter() {
    }
    
    /** Record a hit.
        @param timestamp - The current timestamp (in seconds granularity). */
    void hit(int timestamp) {
        this->hits.push(timestamp);
    }
    
    /** Return the number of hits in the past 5 minutes.
        @param timestamp - The current timestamp (in seconds granularity). */
    int getHits(int timestamp) {
        while (!this->hits.empty()) {
            int diff = timestamp - this->hits.front();
            if (diff >= 300) this->hits.pop();
            else break;
        }
        return this->hits.size();
    }
};
```

**Complexity Analysis**

- Time Complexity
    
    - `hit` - Since inserting a value in the queue takes place in O(1) time, hence `hit` method works in O(1).
        
    - `getHits` - Assuming a total of n values present in the queue at a time and the total number of timestamps encountered throughout is N. In the worst case scenario, we might end up removing all the entries from the queue in `getHits` method if the difference in timestamp is greater than or equal to 300. Hence in the worst case, a "single" call to the `getHits` method can take O(n) time. However, we must notice that each timestamp is processed only twice (first while adding the timestamp in the queue in `hit` method and second while removing the timestamp from the queue in the `getHits` method). Hence if the total number of timestamps encountered throughout is N, the overall time taken by `getHits` method is O(N). This results in an amortized time complexity of O(1) for a single call to `getHits` method.
        
- Space Complexity: Considering the total timestamps encountered throughout to be N, the queue can have upto N elements, hence overall space complexity of this approach is O(N).
    

### Approach #2: Using Deque with Pairs

Consider the follow up, where we have multiple hits arriving at the "same" timestamps. We can optimize Approach 1 even further. In this approach, we'll not only keep the timestamps but will also keep the count of the timestamps as well. For example, if we call `hit` method 5 times for `timestamp = 1`, the queue in case of Approach 1 will look like `[1, 1, 1, 1, 1]`. This will lead to 5 removals in the `getHits` method when we remove the value `1` from the queue. To avoid this repetitive removals of the same value, in Approach 2, we'll store the value as `(1, 5)` where the first value 1 is the timestamp and the second value `5` is the count. For this, we'll use the "deque" data structure which allows us to insert and delete values from both the ends of the queue.

**Algorithm**

The updated algorithm in Approach 2 is as follows.

- If we encounter the hit for the same timestamp, instead of appending a new entry in the deque, we simply increment the count of the latest timestamp.
    
- In order to keep the track of total number of elements (for the last 300 seconds), we also use a variable `total` which we initialize to `0` and keep updating as we add or remove the elements from the queue. We increment the value of `total` by 1 when `hit` method is called and we decrement by the value of `total` by the count of the timestamp that we remove from the queue.
    

Below is the implementation of this approach.
```c++
class HitCounter {
private:
    
    int total;
    queue<pair<int, int> > hits;
    
public:
    
    /** Initialize your data structure here. */
    HitCounter() {
        this->total = 0;
    }
    
    /** Record a hit.
        @param timestamp - The current timestamp (in seconds granularity). */
    void hit(int timestamp) {
        if (this->hits.empty() || this->hits.back().first != timestamp) {
            // Insert the new timestamp with count = 1
            this->hits.push({timestamp, 1});
        } else {
            // Update the count of latest timestamp by incrementing the count by 1
            this->hits.back().second++;
        }
        this->total++;
    }
    
    /** Return the number of hits in the past 5 minutes.
        @param timestamp - The current timestamp (in seconds granularity). */
    int getHits(int timestamp) {
        while (!this->hits.empty()) {
            int diff = timestamp - this->hits.front().first;
            if (diff >= 300) {
                // Decrement total by the count of the oldest timestamp
                this->total -= this->hits.front().second;
                this->hits.pop();
            }
            else break;
        }
        return this->total;
    }
};
```

**Complexity Analysis**

In the worst case, when there are not many repetitions, the time complexity and space complexity of Approach 2 is the same as Approach 1. However in case we have repetitions (say k repetitions of a particular ith timestamp), the time complexity and space complexities are as follows.

- Time Complexity:
    
    - `hit` - O(1).
        
    - `getHits` - If there are a total of n pairs present in the deque, worst case time complexity can be O(n). However, by clubbing all the timestamps with same value together, for the ith timestamp with k repetitions, the time complexity is O(1) as here, instead of removing all those k repetitions, we only remove a single entry from the deque.
        
- Space complexity: If there are a total of N elements that we encountered throughout, the space complexity is O(N) (similar to Approach 1). However, in the case of repetitions, the space required for storing those k values O(1).


## Other approaches
---
O(s) s is total seconds in given time interval, in this case 300.  
basic ideal is using buckets. 1 bucket for every second because we only need to keep the recent hits info for 300 seconds. hit[] array is wrapped around by mod operation. Each hit bucket is associated with times[] bucket which record current time. If it is not current time, it means it is 300s or 600s... ago and need to reset to 1.

```csharp
public class HitCounter {
    private int[] times;
    private int[] hits;
    /** Initialize your data structure here. */
    public HitCounter() {
        times = new int[300];
        hits = new int[300];
    }
    
    /** Record a hit.
        @param timestamp - The current timestamp (in seconds granularity). */
    public void hit(int timestamp) {
        int index = timestamp % 300;
        if (times[index] != timestamp) {
            times[index] = timestamp;
            hits[index] = 1;
        } else {
            hits[index]++;
        }
    }
    
    /** Return the number of hits in the past 5 minutes.
        @param timestamp - The current timestamp (in seconds granularity). */
    public int getHits(int timestamp) {
        int total = 0;
        for (int i = 0; i < 300; i++) {
            if (timestamp - times[i] < 300) {
                total += hits[i];
            }
        }
        return total;
    }
}
```
---
