# Tasks with intervals

+ [Non-overlapping Intervals](#non-overlapping-intervals)
+ [Merge Intervals](#merge-intervals)
+ [Insert Interval](#insert-interval)

## Non-overlapping Intervals

https://leetcode.com/problems/non-overlapping-intervals/

```C++
class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        int size = intervals.size();
        if(!size)
            return 0;
        sort(intervals.begin(), intervals.end());
        int prev_end = intervals[0][1];
        int result = 0;
        for(int i = 1; i < size; i++){
            if(intervals[i][0] < prev_end){
                result++;
                prev_end = min(intervals[i][1], prev_end);
            }
            else
                prev_end = intervals[i][1];
        }
        return result;
    }
};
```

## Merge Intervals

https://leetcode.com/problems/merge-intervals/

```C++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        int size = intervals.size();
        if(!size)
            return intervals;
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> newIntervals;
        newIntervals.push_back(intervals[0]); 
        for(int i = 1; i < size; i++){
            if(intervals[i][0] <= newIntervals[newIntervals.size() - 1][1])
                newIntervals[newIntervals.size() - 1][1] = max(intervals[i][1], newIntervals[newIntervals.size() - 1][1]);
            else
               newIntervals.push_back(intervals[i]); 
        }
        return newIntervals;
    }
};
```

## Insert Interval

https://leetcode.com/problems/insert-interval/

```C++
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        int size = intervals.size();
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> newIntervals;
        int i = 0;
        while(i < size && intervals[i][1] < newInterval[0]){
            newIntervals.push_back(intervals[i]); 
            i++;
        }
        newIntervals.push_back(newInterval);
        if(i < size && intervals[i][0] <= newIntervals[newIntervals.size() - 1][1])
            newIntervals[newIntervals.size() - 1][0] = min(newInterval[0], intervals[i][0]);
        while(i < size && intervals[i][0] <= newIntervals[newIntervals.size() - 1][1]){
            newIntervals[newIntervals.size() - 1][1] = max(intervals[i][1], newInterval[1]); 
            i++;
        }
        for(i; i < size; i++)
            newIntervals.push_back(intervals[i]); 
        return newIntervals;
    }
};
```
