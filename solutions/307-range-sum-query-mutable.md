# Problem 307: Range Sum Query - Mutable

## Problem Statement
Given an integer array `nums`, handle multiple queries of the following types:
1. Update the value of an element in `nums`.
2. Calculate the sum of the elements of `nums` between indices `left` and `right` inclusive.

## Binary Indexed Tree (Fenwick Tree)
- `update(i, delta)`: Add delta to index `i`, increment `i += i & -i`.
- `query(i)`: Sum up values, decrement `i -= i & -i`.
- Range sum: `query(right) - query(left - 1)`.

## Complexity
- Point Update: $O(\log N)$
- Range Query: $O(\log N)$
- Construction: $O(N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>

class NumArray {
    std::vector<int> bit;
    std::vector<int> elements;
    int n;

    void add(int i, int delta) {
        for (; i <= n; i += i & -i) {
            bit[i] += delta;
        }
    }

    int prefixSum(int i) const {
        int sum = 0;
        for (; i > 0; i -= i & -i) {
            sum += bit[i];
        }
        return sum;
    }

public:
    NumArray(std::vector<int>& nums) : elements(nums), n(nums.size()), bit(nums.size() + 1, 0) {
        for (int i = 0; i < n; ++i) {
            add(i + 1, nums[i]);
        }
    }

    void update(int index, int val) {
        int delta = val - elements[index];
        elements[index] = val;
        add(index + 1, delta);
    }

    int sumRange(int left, int right) const {
        return prefixSum(right + 1) - prefixSum(left);
    }
};
```
