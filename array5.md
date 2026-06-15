# 50. Pow(x, n)

## Problem Statement

Implement `pow(x, n)`, which calculates `x` raised to the power `n` (`xⁿ`).

**LeetCode Link:** https://leetcode.com/problems/powx-n/

---

## Approach

We use **Binary Exponentiation (Fast Power)** to efficiently compute the result.

### Key Idea
- If `n` is even:
  - `xⁿ = (x²)^(n/2)`
- If `n` is odd:
  - Multiply the result by `x` and reduce the exponent.
- Handle negative powers by computing the reciprocal.

This reduces the time complexity from **O(n)** to **O(log n)**.

---

## Algorithm

1. Convert `n` to `long long` to avoid overflow.
2. If `n` is negative:
   - Take reciprocal of `x`.
   - Make `n` positive.
3. Repeatedly:
   - If exponent is odd, multiply answer by current base.
   - Square the base.
   - Divide exponent by 2.
4. Return the answer.

---

## C++ Solution

```cpp
class Solution {
public:
    double myPow(double x, int n) {
        long long power = n;
        
        if (power < 0) {
            x = 1 / x;
            power = -power;
        }

        double ans = 1.0;

        while (power > 0) {
            if (power % 2 == 1) {
                ans *= x;
            }

            x *= x;
            power /= 2;
        }

        return ans;
    }
};
```

---

## Complexity Analysis

- **Time Complexity:** O(log n)
- **Space Complexity:** O(1)

---

## Topics

- Binary Search
- Binary Exponentiation
- Recursion & Divide and Conquer
- Math

---

## Example

**Input:**
```text
x = 2.00000, n = 10
```

**Output:**
```text
1024.00000
```

**Explanation:**
```text
2^10 = 1024
```

---
⭐ Efficient solution using Binary Exponentiation.
