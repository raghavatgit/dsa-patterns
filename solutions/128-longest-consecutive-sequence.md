# Problem 128: Longest Consecutive Sequence

## Problem Statement
Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence in $O(N)$ time.

## Algorithm
Insert all elements into an unordered hash set.
Iterate through numbers: only start counting if `x - 1` is not in the set (guaranteeing `x` is the streak root).
Increment `curr = x + 1` while present in set. Update `max_streak`.

## Complexity
- Time: $O(N)$ each element visited at most twice.
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <unordered_set>
#include <algorithm>

int longestConsecutive(const std::vector<int>& nums) {
    std::unordered_set<int> num_set(nums.begin(), nums.end());
    int max_streak = 0;

    for (int num : num_set) {
        if (!num_set.count(num - 1)) {
            int curr = num;
            int streak = 1;

            while (num_set.count(curr + 1)) {
                curr++;
                streak++;
            }
            max_streak = std::max(max_streak, streak);
        }
    }
    return max_streak;
}
```
