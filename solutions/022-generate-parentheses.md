# 22. Generate Parentheses

## Complexity
- Time Complexity: O(4^n / sqrt(n)) Catalan number
- Space Complexity: O(n) recursion stack

## Rust Implementation
```rust
pub fn generate_parenthesis(n: i32) -> Vec<String> {
    let mut res = Vec::new();
    let mut curr = String::with_capacity((2 * n) as usize);

    fn backtrack(open: i32, close: i32, n: i32, curr: &mut String, res: &mut Vec<String>) {
        if curr.len() == (2 * n) as usize {
            res.push(curr.clone());
            return;
        }
        if open < n {
            curr.push('(');
            backtrack(open + 1, close, n, curr, res);
            curr.pop();
        }
        if close < open {
            curr.push(')');
            backtrack(open, close + 1, n, curr, res);
            curr.pop();
        }
    }

    backtrack(0, 0, n, &mut curr, &mut res);
    res
}
```
