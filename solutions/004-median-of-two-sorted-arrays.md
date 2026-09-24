# Problem 004: Median of Two Sorted Arrays

## Problem Statement
Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the median of the two sorted arrays. The overall run time complexity should be $O(\log(m+n))$.

## Binary Search Partition
Binary search on the smaller array `nums1` of size $M$.
Partition index $i$ in `nums1` and $j = (M + N + 1)/2 - i$ in `nums2`.
Valid partition condition:
$$nums1[i - 1] \le nums2[j] \quad \text{and} \quad nums2[j - 1] \le nums1[i]$$

## Complexity
- Time: $O(\log(\min(M, N)))$
- Space: $O(1)$

## C++ Implementation
```cpp
#include <vector>
#include <algorithm>
#include <climits>

double findMedianSortedArrays(const std::vector<int>& nums1, const std::vector<int>& nums2) {
    if (nums1.size() > nums2.size()) return findMedianSortedArrays(nums2, nums1);

    int m = nums1.size();
    int n = nums2.size();
    int low = 0, high = m;

    while (low <= high) {
        int i = low + (high - low) / 2;
        int j = (m + n + 1) / 2 - i;

        int max_left1 = (i == 0) ? INT_MIN : nums1[i - 1];
        int min_right1 = (i == m) ? INT_MAX : nums1[i];

        int max_left2 = (j == 0) ? INT_MIN : nums2[j - 1];
        int min_right2 = (j == n) ? INT_MAX : nums2[j];

        if (max_left1 <= min_right2 && max_left2 <= min_right1) {
            if ((m + n) % 2 == 0) {
                return (std::max(max_left1, max_left2) + std::min(min_right1, min_right2)) / 2.0;
            } else {
                return std::max(max_left1, max_left2);
            }
        } else if (max_left1 > min_right2) {
            high = i - 1;
        } else {
            low = i + 1;
        }
    }
    return 0.0;
}
```
