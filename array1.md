# 169. Majority Element

## Problem Link

🔗 https://leetcode.com/problems/majority-element/

---

## Problem Statement

Given an array `nums` of size `n`, return the **majority element**.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

---

## Examples

### Example 1

```text
Input: nums = [3,2,3]
Output: 3
```

### Example 2

```text
Input: nums = [2,2,1,1,1,2,2]
Output: 2
```

---

## Approach

### Boyer-Moore Voting Algorithm

The key observation is that the majority element appears more than half of the total elements.

We maintain:

- `candidate` → potential majority element.
- `count` → tracks the balance of occurrences.

### Steps

1. Initialize `count = 0`.
2. Traverse the array.
3. If `count == 0`, choose the current element as the new candidate.
4. If the current element equals the candidate, increment `count`.
5. Otherwise, decrement `count`.
6. After the traversal, the candidate will be the majority element.

### Why It Works?

Since the majority element appears more than `n/2` times, it cannot be completely canceled out by the remaining elements. Therefore, the final candidate is guaranteed to be the majority element.

---

## C++ Solution

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int candidate = 0;
        int count = 0;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }

            if (num == candidate) {
                count++;
            } else {
                count--;
            }
        }

        return candidate;
    }
};
```

---

## Dry Run

### Input

```text
nums = [2,2,1,1,1,2,2]
```

| Element | Candidate | Count |
| -------- | --------- | ----- |
| 2 | 2 | 1 |
| 2 | 2 | 2 |
| 1 | 2 | 1 |
| 1 | 2 | 0 |
| 1 | 1 | 1 |
| 2 | 1 | 0 |
| 2 | 2 | 1 |

Final Candidate = **2**

### Output

```text
2
```

---

## Complexity Analysis

### Time Complexity

```text
O(n)
```

Single traversal of the array.

### Space Complexity

```text
O(1)
```

Only two variables (`candidate` and `count`) are used.

---

## Key Takeaway

The Boyer-Moore Voting Algorithm is the most optimal solution for this problem because it finds the majority element in **O(n)** time using **O(1)** extra space.
