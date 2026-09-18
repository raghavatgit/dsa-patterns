# Problem: Count of Smaller Numbers After Self

## Problem Statement
Given an integer array `nums`, return an integer array `counts` where `counts[i]` is the number of smaller elements to the right of `nums[i]`.

## Intuition & Approach
Modified Merge Sort Inversion Counting:
1. Associate each element with its original index: `(val, original_idx)`.
2. Perform merge sort dividing array into left and right sorted halves.
3. During the merge step:
   - When placing an element from the left half into the merged array, count how many elements from the right half have already been placed before it (those elements are smaller and originally appeared to its right).
   - Increment `counts[left_element.original_idx] += right_elements_placed`.
4. Time Complexity: $O(N \log N)$ strictly bounded by merge sort. Space Complexity: $O(N)$ temporary merge buffers.

## TypeScript Implementation

```typescript
interface Item {
  val: number;
  idx: number;
}

export function countSmaller(nums: number[]): number[] {
  const n = nums.length;
  const counts: number[] = new Array(n).fill(0);
  const items: Item[] = nums.map((val, idx) => ({ val, idx }));

  function mergeSort(arr: Item[], left: number, right: number) {
    if (left >= right) return;
    const mid = left + Math.floor((right - left) / 2);
    mergeSort(arr, left, mid);
    mergeSort(arr, mid + 1, right);

    const temp: Item[] = [];
    let l = left;
    let r = mid + 1;
    let rightCount = 0;

    while (l <= mid && r <= right) {
      if (arr[r].val < arr[l].val) {
        rightCount++;
        temp.push(arr[r++]);
      } else {
        counts[arr[l].idx] += rightCount;
        temp.push(arr[l++]);
      }
    }

    while (l <= mid) {
      counts[arr[l].idx] += rightCount;
      temp.push(arr[l++]);
    }

    while (r <= right) {
      temp.push(arr[r++]);
    }

    for (let i = 0; i < temp.length; i++) {
      arr[left + i] = temp[i];
    }
  }

  mergeSort(items, 0, n - 1);
  return counts;
}
```
