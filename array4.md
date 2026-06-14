# 50. Pow(x, n)

## Problem Statement
Implement `pow(x, n)`, which calculates `x` raised to the power `n` (`x^n`).

**LeetCode Link:** https://leetcode.com/problems/powx-n/

---

## Approach
Use **Binary Exponentiation (Fast Power)**.

Instead of multiplying `x` by itself `n` times, repeatedly:
- If `n` is odd, multiply the answer by `x`.
- Square `x`.
- Divide `n` by 2.

For negative powers:
- Convert `n` to a positive value.
- Compute the power.
- Return its reciprocal.

---

## C++ Solution

```cpp
class Solution {
public:
    double myPow(double x, int n) {
        long long N = n;

        if (N < 0) {
            x = 1 / x;
            N = -N;
        }

        double ans = 1.0;

        while (N > 0) {
            if (N & 1)
                ans *= x;

            x *= x;
            N >>= 1;
        }

        return ans;
    }
};
