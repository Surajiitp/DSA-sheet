# 56. Merge Intervals

## 🔗 Problem Link
https://leetcode.com/problems/merge-intervals/

## 📖 Problem Statement

Given an array of intervals where `intervals[i] = [starti, endi]`, merge all overlapping intervals and return an array of the non-overlapping intervals that cover all the intervals in the input.

---

## 📝 Examples

### Example 1

```text
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
```

### Example 2

```text
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
```

---

## 💡 Approach

1. Sort the intervals based on their starting point.
2. Maintain the current interval using `start` and `end`.
3. Traverse through all intervals:
   - If the current interval overlaps with the previous one, merge them by updating the end.
   - Otherwise, add the previous interval to the answer and start a new interval.
4. Add the last interval to the result.

---

## 🚀 C++ Solution

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());

        vector<vector<int>> ans;

        int start = intervals[0][0];
        int end = intervals[0][1];

        for (int i = 1; i < intervals.size(); i++) {
            if (intervals[i][0] <= end) {
                end = max(end, intervals[i][1]);
            } else {
                ans.push_back({start, end});
                start = intervals[i][0];
                end = intervals[i][1];
            }
        }

        ans.push_back({start, end});

        return ans;
    }
};
```

---

## 🔍 Dry Run

### Input

```text
[[1,3],[2,6],[8,10],[15,18]]
```

### Sorted Intervals

```text
[[1,3],[2,6],[8,10],[15,18]]
```

### Processing

```text
[1,3] and [2,6] overlap
=> [1,6]

[8,10] does not overlap
=> Add [1,6]

[15,18] does not overlap
=> Add [8,10]

Final Answer:
[[1,6],[8,10],[15,18]]
```

---

## ⏱️ Complexity Analysis

| Complexity | Value |
|------------|--------|
| Time       | O(n log n) |
| Space      | O(1) (excluding output) |

---

## 🏷️ Tags

- Array
- Sorting
- Intervals

## ⭐ Difficulty

Medium
