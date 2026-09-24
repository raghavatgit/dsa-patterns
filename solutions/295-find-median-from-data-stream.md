# Problem 295: Find Median from Data Stream

## Problem Statement
The median is the middle value in an ordered integer list. Implement the `MedianFinder` class with $O(\log N)$ insertion and $O(1)$ median lookup.

## Two-Heap Balance
- `left` max-heap stores smaller half of elements.
- `right` min-heap stores larger half of elements.
- Invariant: `left.size() == right.size()` or `left.size() == right.size() + 1`.

## Complexity
- `addNum`: $O(\log N)$
- `findMedian`: $O(1)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <queue>
#include <vector>

class MedianFinder {
    std::priority_queue<int> left; // Max-heap
    std::priority_queue<int, std::vector<int>, std::greater<int>> right; // Min-heap

public:
    MedianFinder() {}

    void addNum(int num) {
        left.push(num);
        right.push(left.top());
        left.pop();

        if (right.size() > left.size()) {
            left.push(right.top());
            right.pop();
        }
    }

    double findMedian() const {
        if (left.size() > right.size()) {
            return left.top();
        }
        return (left.top() + right.top()) / 2.0;
    }
};
```
