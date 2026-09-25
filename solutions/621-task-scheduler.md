# 621. Task Scheduler

## Problem Statement
Given a characters array `tasks`, representing the tasks a CPU needs to do, where each letter represents a different task. Tasks could be done in any order. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.

However, there is a non-negative integer `n` that represents the cooldown period between two same tasks. Return the minimum number of units of times that the CPU will take to finish all the given tasks.

---

## Method Explanation
1. Find maximum task frequency `max_freq`.
2. Count how many tasks share this maximum frequency: `max_count`.
3. Frame structure has `max_freq - 1` chunks of size `n + 1`, plus `max_count` elements in the final incomplete chunk.
4. Total required slots = `max(tasks.len(), (max_freq - 1) * (n + 1) + max_count)`.

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn least_interval(tasks: Vec<char>, n: i32) -> i32 {
        let mut counts = [0i32; 26];
        for t in &tasks {
            counts[(*t as u8 - b'A') as usize] += 1;
        }

        let max_freq = *counts.iter().max().unwrap();
        let max_count = counts.iter().filter(|&&c| c == max_freq).count() as i32;

        let empty_slots = (max_freq - 1) * (n + 1) + max_count;
        empty_slots.max(tasks.len() as i32)
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_task_scheduler() {
        assert_eq!(
            Solution::least_interval(vec!['A', 'A', 'A', 'B', 'B', 'B'], 2),
            8
        );
        assert_eq!(
            Solution::least_interval(vec!['A', 'A', 'A', 'B', 'B', 'B'], 0),
            6
        );
    }
}
```

---

## Complexity Analysis
- Time Complexity: `O(N)` to count frequencies.
- Space Complexity: `O(1)` fixed 26-element array.
