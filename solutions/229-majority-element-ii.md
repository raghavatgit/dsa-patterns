# Problem: Majority Element II

## Problem Statement
Given an integer array of size `n`, find all elements that appear more than $\lfloor n / 3 \rfloor$ times.

## Intuition & Approach
Generalized Boyer-Moore with 2 Candidates:
1. There can be at most 2 elements appearing more than $\lfloor N / 3 \rfloor$ times.
2. Pass 1: Maintain two candidates `cand1`, `cand2` with counters `count1`, `count2`.
3. Pass 2: Verify frequency of candidates across array to confirm $> N / 3$.
4. Time Complexity: $2 \times O(N) = O(N)$. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function majorityElementII(nums: number[]): number[] {
  let cand1: number | null = null;
  let cand2: number | null = null;
  let count1 = 0;
  let count2 = 0;

  for (const num of nums) {
    if (cand1 !== null && num === cand1) {
      count1++;
    } else if (cand2 !== null && num === cand2) {
      count2++;
    } else if (count1 === 0) {
      cand1 = num;
      count1 = 1;
    } else if (count2 === 0) {
      cand2 = num;
      count2 = 1;
    } else {
      count1--;
      count2--;
    }
  }

  // Verification pass
  let freq1 = 0;
  let freq2 = 0;
  for (const num of nums) {
    if (num === cand1) freq1++;
    else if (num === cand2) freq2++;
  }

  const result: number[] = [];
  const threshold = Math.floor(nums.length / 3);
  if (freq1 > threshold && cand1 !== null) result.push(cand1);
  if (freq2 > threshold && cand2 !== null) result.push(cand2);

  return result;
}
```
