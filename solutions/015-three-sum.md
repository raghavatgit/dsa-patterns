# Problem: Three Sum

## Problem Statement
Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`. The solution set must not contain duplicate triplets.

## Intuition & Approach
1. Sort the array in ascending order.
2. Fix the first element `nums[i]`. If `nums[i] > 0`, break early (triplet sum cannot be zero).
3. Use two converging pointers `left = i + 1` and `right = n - 1`.
4. Skip duplicate elements for `i`, `left`, and `right` to ensure unique triplets.

## TypeScript Implementation

```typescript
export function threeSum(nums: number[]): [number, number, number][] {
  const result: [number, number, number][] = [];
  nums.sort((a, b) => a - b);

  for (let i = 0; i < nums.length - 2; i++) {
    if (nums[i] > 0) break;
    if (i > 0 && nums[i] === nums[i - 1]) continue; // Skip duplicate i

    let left = i + 1;
    let right = nums.length - 1;

    while (left < right) {
      const sum = nums[i] + nums[left] + nums[right];

      if (sum === 0) {
        result.push([nums[i], nums[left], nums[right]]);
        while (left < right && nums[left] === nums[left + 1]) left++;
        while (left < right && nums[right] === nums[right - 1]) right--;
        left++;
        right--;
      } else if (sum < 0) {
        left++;
      } else {
        right--;
      }
    }
  }

  return result;
}
```

## Rust Implementation

```rust
pub fn three_sum(mut nums: Vec<i32>) -> Vec<Vec<i32>> {
    let mut result = Vec::new();
    nums.sort_unstable();

    for i in 0..nums.len().saturating_sub(2) {
        if nums[i] > 0 {
            break;
        }
        if i > 0 && nums[i] == nums[i - 1] {
            continue;
        }

        let mut left = i + 1;
        let mut right = nums.len() - 1;

        while left < right {
            let sum = nums[i] + nums[left] + nums[right];
            match sum.cmp(&0) {
                std::cmp::Ordering::Equal => {
                    result.push(vec![nums[i], nums[left], nums[right]]);
                    while left < right && nums[left] == nums[left + 1] {
                        left += 1;
                    }
                    while left < right && nums[right] == nums[right - 1] {
                        right -= 1;
                    }
                    left += 1;
                    right -= 1;
                }
                std::cmp::Ordering::Less => left += 1,
                std::cmp::Ordering::Greater => right -= 1,
            }
        }
    }

    result
}
```

## Complexity Analysis
* **Time Complexity:** O(N^2) sorting takes O(N log N) followed by O(N) two-pointer scans for each element.
* **Space Complexity:** O(1) auxiliary space (excluding result container).
