# 150. Evaluate Reverse Polish Notation

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn eval_rpn(tokens: Vec<String>) -> i32 {
    let mut stack = Vec::new();
    for token in tokens {
        match token.as_str() {
            "+" => { let b = stack.pop().unwrap(); let a = stack.pop().unwrap(); stack.push(a + b); }
            "-" => { let b = stack.pop().unwrap(); let a = stack.pop().unwrap(); stack.push(a - b); }
            "*" => { let b = stack.pop().unwrap(); let a = stack.pop().unwrap(); stack.push(a * b); }
            "/" => { let b = stack.pop().unwrap(); let a = stack.pop().unwrap(); stack.push(a / b); }
            num => stack.push(num.parse::<i32>().unwrap()),
        }
    }
    stack.pop().unwrap()
}
```
