# 53. Maximum Subarray

## Problem

Given an integer array `nums`, find the contiguous subarray with the largest sum and return its sum.

---

## Example 1

Input:
```cpp
nums = [-2,1,-3,4,-1,2,1,-5,4]
```

Output:
```cpp
6
```

Explanation:
```cpp
[4,-1,2,1] => 6
```

---

## Example 2

Input:
```cpp
nums = [1]
```

Output:
```cpp
1
```

---

## Example 3

Input:
```cpp
nums = [5,4,-1,7,8]
```

Output:
```cpp
23
```

---

## Approach (Kadane's Algorithm)

For every element, we have two choices:

1. Start a new subarray from the current element.
2. Extend the previous subarray.

We choose the option that gives the maximum sum.

```cpp
currSum = max(nums[i], currSum + nums[i]);
```

Then update the overall maximum:

```cpp
maxSum = max(maxSum, currSum);
```

---

## C++ Solution

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {

        int currSum = nums[0];
        int maxSum = nums[0];

        for (int i = 1; i < nums.size(); i++) {

            currSum = max(nums[i], currSum + nums[i]);

            maxSum = max(maxSum, currSum);
        }

        return maxSum;
    }
};
```

---

## Dry Run

```cpp
nums = [-2,1,-3,4,-1,2,1,-5,4]
```

| Index | Value | currSum | maxSum |
|---------|---------|---------|---------|
| 0 | -2 | -2 | -2 |
| 1 | 1 | 1 | 1 |
| 2 | -3 | -2 | 1 |
| 3 | 4 | 4 | 4 |
| 4 | -1 | 3 | 4 |
| 5 | 2 | 5 | 5 |
| 6 | 1 | 6 | 6 |
| 7 | -5 | 1 | 6 |
| 8 | 4 | 5 | 6 |

Final Answer:

```cpp
6
```

---

## Complexity Analysis

### Time Complexity

```cpp
O(n)
```

### Space Complexity

```cpp
O(1)
```

---

## Key Takeaway

Kadane's Algorithm helps find the maximum subarray sum in a single traversal by deciding at every index whether to:

```cpp
Start New Subarray
OR
Extend Previous Subarray
```

---

## Topics

- Array
- Dynamic Programming
- Greedy
- Kadane's Algorithm
