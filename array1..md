# 15. 3Sum

## Problem Statement

Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that:

- `i != j`
- `i != k`
- `j != k`
- `nums[i] + nums[j] + nums[k] == 0`

The solution set must not contain duplicate triplets.

### Example 1

**Input:**
```cpp
nums = [-1,0,1,2,-1,-4]
```

**Output:**
```cpp
[[-1,-1,2],[-1,0,1]]
```

### Example 2

**Input:**
```cpp
nums = [0,1,1]
```

**Output:**
```cpp
[]
```

---

## Approach (Sorting + Two Pointers)

1. Sort the array.
2. Fix one element using a loop.
3. Use two pointers:
   - `left = i + 1`
   - `right = n - 1`
4. Calculate the sum:
   - If sum = 0 → store triplet.
   - If sum < 0 → move left pointer.
   - If sum > 0 → move right pointer.
5. Skip duplicate elements to avoid repeated triplets.

---

## C++ Solution

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> ans;

        sort(nums.begin(), nums.end());

        for (int i = 0; i < nums.size(); i++) {

            if (i > 0 && nums[i] == nums[i - 1])
                continue;

            int j = i + 1;
            int k = nums.size() - 1;

            while (j < k) {

                int sum = nums[i] + nums[j] + nums[k];

                if (sum == 0) {

                    ans.push_back({nums[i], nums[j], nums[k]});

                    j++;
                    k--;

                    while (j < k && nums[j] == nums[j - 1])
                        j++;

                    while (j < k && nums[k] == nums[k + 1])
                        k--;
                }
                else if (sum < 0) {
                    j++;
                }
                else {
                    k--;
                }
            }
        }

        return ans;
    }
};
```

---

## Dry Run

### Input

```cpp
[-1,0,1,2,-1,-4]
```

### After Sorting

```cpp
[-4,-1,-1,0,1,2]
```

### Valid Triplets

```cpp
[-1,-1,2]
[-1,0,1]
```

### Output

```cpp
[[-1,-1,2],[-1,0,1]]
```

---

## Complexity Analysis

### Time Complexity

```cpp
O(n²)
```

- Sorting: `O(n log n)`
- Two Pointer Traversal: `O(n²)`

Overall:

```cpp
O(n²)
```

### Space Complexity

```cpp
O(1)
```

(Excluding the output array)

---

## Key Concepts

- Sorting
- Two Pointers
- Array Traversal
- Duplicate Handling
- Optimization from O(n³) to O(n²)

---

## LeetCode Link

https://leetcode.com/problems/3sum/

## Tags

`Array` `Two Pointers` `Sorting`
