# 3. Longest Substring Without Repeating Characters

## Problem Statement

Given a string `s`, find the length of the longest substring without repeating characters.

**LeetCode Link:** https://leetcode.com/problems/longest-substring-without-repeating-characters/

---

## Example 1

**Input**

```text
s = "abcabcbb"
```

**Output**

```text
3
```

**Explanation**

The answer is `"abc"`, with length `3`.

---

## Example 2

**Input**

```text
s = "bbbbb"
```

**Output**

```text
1
```

---

## Example 3

**Input**

```text
s = "pwwkew"
```

**Output**

```text
3
```

**Explanation**

The answer is `"wke"`.

---

## Intuition

Maintain a sliding window that always contains unique characters.

- Expand the window by moving the right pointer.
- If a character repeats, move the left pointer just after its last occurrence.
- Track the maximum window size.

---

## Algorithm

1. Create an array to store the last occurrence of each character.
2. Initialize `left = 0`.
3. Traverse the string using `right`.
4. If the current character is already inside the window:
   - Move `left` to `lastOccurrence + 1`.
5. Update the last occurrence of the current character.
6. Update the maximum length.

---

## C++ Solution

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> last(128, -1);

        int left = 0;
        int ans = 0;

        for (int right = 0; right < s.size(); right++) {
            if (last[s[right]] >= left)
                left = last[s[right]] + 1;

            last[s[right]] = right;
            ans = max(ans, right - left + 1);
        }

        return ans;
    }
};
```

---

## Dry Run

### Input

```text
s = "abcabcbb"
```

| Right | Character | Left | Current Window | Max Length |
|------:|:---------:|-----:|:--------------:|-----------:|
| 0 | a | 0 | a | 1 |
| 1 | b | 0 | ab | 2 |
| 2 | c | 0 | abc | 3 |
| 3 | a | 1 | bca | 3 |
| 4 | b | 2 | cab | 3 |
| 5 | c | 3 | abc | 3 |
| 6 | b | 5 | cb | 3 |
| 7 | b | 7 | b | 3 |

Final Answer:

```text
3
```

---

## Complexity Analysis

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(128)` ≈ `O(1)`

---

## Why This Works

- Each character is processed at most twice (once by `right`, once by `left`).
- The sliding window always contains unique characters.
- This guarantees a linear-time solution.

---

## Topics

- Hash Table
- String
- Sliding Window
- Two Pointers

---

## Tags

`Hash Table` `String` `Sliding Window` `Two Pointers`
