# Problem 239: Sliding Window Maximum

## Problem Statement
You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

## Approach
Monotonic Deque (Decreasing):
1. Store indices in deque.
2. Evict indices outside current window: `front <= i - k`.
3. Maintain decreasing order: while `!deque.empty() && nums[deque.back()] <= nums[i]`, pop back.
4. Front of deque always holds maximum element index in current window.

## Complexity
- Time Complexity: $O(N)$ as each index is pushed and popped at most once.
- Space Complexity: $O(k)$ for deque storage.

## C++ Implementation
```cpp
#include <vector>
#include <deque>

std::vector<int> maxSlidingWindow(const std::vector<int>& nums, int k) {
    std::deque<int> dq;
    std::vector<int> result;
    result.reserve(nums.size() - k + 1);

    for (int i = 0; i < static_cast<int>(nums.size()); ++i) {
        if (!dq.empty() && dq.front() <= i - k) {
            dq.pop_front();
        }

        while (!dq.empty() && nums[dq.back()] <= nums[i]) {
            dq.pop_back();
        }

        dq.push_back(i);

        if (i >= k - 1) {
            result.push_back(nums[dq.front()]);
        }
    }
    return result;
}
```
