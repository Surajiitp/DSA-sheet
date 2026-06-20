# LeetCode 11 - Container With Most Water

## Problem Statement

You are given an integer array `height` where each element represents the height of a vertical line.

Find two lines that together with the x-axis form a container such that the container stores the **maximum amount of water**.

Return the maximum amount of water the container can contain.

---

## Example

### Input

```cpp
height = [1,8,6,2,5,4,8,3,7]
```

### Output

```cpp
49
```

### Explanation

```text
Left Height  = 8
Right Height = 7

Width = 8 - 1 = 7

Area = min(8, 7) × 7
     = 7 × 7
     = 49
```

---

## Intuition

The area formed by two lines is:

```text
Area = min(height[left], height[right]) × (right - left)
```

- Height is determined by the smaller line.
- Width is the distance between the two lines.

To maximize area:

- Start with maximum width.
- Calculate area.
- Move the pointer with the smaller height because only increasing the smaller height can potentially increase the area.

---

## Approach: Two Pointers

### Steps

1. Place `left` at index `0`.
2. Place `right` at index `n - 1`.
3. Calculate:
   - `height = min(height[left], height[right])`
   - `width = right - left`
   - `area = height × width`
4. Update maximum area.
5. Move the pointer having smaller height.
6. Repeat until `left >= right`.

---

## C++ Solution

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {

        int left = 0;
        int right = height.size() - 1;
        int maxArea = 0;

        while(left < right) {

            int h = min(height[left], height[right]);
            int w = right - left;

            int area = h * w;

            maxArea = max(maxArea, area);

            if(height[left] < height[right]) {
                left++;
            }
            else {
                right--;
            }
        }

        return maxArea;
    }
};
```

---

## Complexity Analysis

### Time Complexity

```text
O(n)
```

### Space Complexity

```text
O(1)
```


## Key Takeaway

Whenever you see:

```text
Two ends of an array
+
Need maximum/minimum value
+
Distance between indices matters
```

Think of **Two Pointers** first. 🚀
