# LeetCode 121 - Best Time to Buy and Sell Stock

## Problem Statement

You are given an array `prices` where `prices[i]` is the price of a stock on the `i-th` day.

You want to maximize your profit by choosing a single day to buy one stock and a different day in the future to sell that stock.

Return the maximum profit you can achieve. If no profit can be made, return `0`.

## Example

### Input
```text
prices = [7,1,5,3,6,4]
```

### Output
```text
5
```

### Explanation
Buy on day 2 at price `1` and sell on day 5 at price `6`.

Profit = `6 - 1 = 5`.

---

## Approach

Maintain:

- `minPrice` → minimum stock price seen so far.
- `maxProfit` → maximum profit obtained so far.

For each price:
1. Update `minPrice`.
2. Calculate profit if selling today.
3. Update `maxProfit`.

This allows us to find the answer in a single pass.

---

## C++ Solution

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int minPrice = INT_MAX;
        int maxProfit = 0;

        for (int price : prices) {
            minPrice = min(minPrice, price);
            maxProfit = max(maxProfit, price - minPrice);
        }

        return maxProfit;
    }
};
```

---

## Complexity Analysis

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## Key Insight

For any day, the best buying price is simply the minimum price encountered before that day. By tracking this minimum value, we can efficiently compute the maximum profit in one traversal.
