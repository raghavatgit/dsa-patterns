# 39. Combination Sum

## Complexity
- Time Complexity: O(2^target)
- Space Complexity: O(target)

## Rust Implementation
```rust
pub fn combination_sum(mut candidates: Vec<i32>, target: i32) -> Vec<Vec<i32>> {
    candidates.sort_unstable();
    let mut res = Vec::new();
    let mut curr = Vec::new();

    fn backtrack(cands: &[i32], start: usize, rem: i32, curr: &mut Vec<i32>, res: &mut Vec<Vec<i32>>) {
        if rem == 0 {
            res.push(curr.clone());
            return;
        }
        for i in start..cands.len() {
            if cands[i] > rem { break; }
            curr.push(cands[i]);
            backtrack(cands, i, rem - cands[i], curr, res);
            curr.pop();
        }
    }

    backtrack(&candidates, 0, target, &mut curr, &mut res);
    res
}
```
