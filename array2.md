# 2965. Find Missing and Repeated Values

## Problem Statement

You are given a 0-indexed 2D integer matrix `grid` of size `n x n` containing all numbers from `1` to `n²`.

Exactly:
- One number appears twice.
- One number is missing.

Return the repeated and missing numbers in the form:

```cpp
[repeated, missing]
```

---

## Approach

We use a frequency array to count the occurrences of each number.

### Algorithm

1. Create a frequency array of size `n² + 1`.
2. Traverse the matrix and count each number.
3. Iterate from `1` to `n²`:
   - Frequency = `2` → Repeated number.
   - Frequency = `0` → Missing number.
4. Return the answer.

---

## Dry Run

### Input

```cpp
grid = {{1,3},
        {2,2}};
```

### Frequency Table

| Number | Frequency |
|---------|-----------|
| 1 | 1 |
| 2 | 2 |
| 3 | 1 |
| 4 | 0 |

Repeated = 2

Missing = 4

### Output

```cpp
[2,4]
```

---

## C++ Solution

```cpp
class Solution {
public:
    vector<int> findMissingAndRepeatedValues(vector<vector<int>>& grid) {

        int n = grid.size();
        int total = n * n;

        vector<int> freq(total + 1, 0);

        for(auto &row : grid) {
            for(auto &num : row) {
                freq[num]++;
            }
        }

        int repeat = -1;
        int missing = -1;

        for(int i = 1; i <= total; i++) {
            if(freq[i] == 2)
                repeat = i;

            if(freq[i] == 0)
                missing = i;
        }

        return {repeat, missing};
    }
};
```

---

## Complexity Analysis

### Time Complexity

```cpp
O(n²)
```

- Traversing the matrix: `O(n²)`
- Checking frequencies: `O(n²)`

Overall: `O(n²)`

### Space Complexity

```cpp
O(n²)
```

- Frequency array of size `n² + 1`.

---

## Topics

- Array
- Hashing
- Frequency Count

---

## Key Insight

Since the matrix should contain every number from `1` to `n²` exactly once, counting the frequency of each number immediately reveals:

- The number occurring twice → Repeated.
- The number never occurring → Missing.
