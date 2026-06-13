# 136. Single Number

## Problem Statement
Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

### Example 1
Input:
```text
nums = [2,2,1]
```

Output:
```text
1
```

### Example 2
Input:
```text
nums = [4,1,2,1,2]
```

Output:
```text
4
```

### Example 3
Input:
```text
nums = [1]
```

Output:
```text
1
```

---

## Approach (Bit Manipulation - XOR)

### Key XOR Properties
- `a ^ a = 0`
- `a ^ 0 = a`
- XOR is commutative and associative.

Since every element appears twice, their XOR becomes `0`.
Only the unique element remains.

Example:

```text
[4,1,2,1,2]

4 ^ 1 ^ 2 ^ 1 ^ 2
= 4 ^ (1 ^ 1) ^ (2 ^ 2)
= 4 ^ 0 ^ 0
= 4
```

---

## C++ Solution

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ans = 0;

        for(int i = 0; i < nums.size(); i++) {
            ans ^= nums[i];
        }

        return ans;
    }
};
```

---

## Complexity Analysis

- Time Complexity: **O(n)**
- Space Complexity: **O(1)**

---

## Topics

- Array
- Bit Manipulation
- XOR
