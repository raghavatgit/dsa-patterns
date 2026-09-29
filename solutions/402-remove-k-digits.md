# 402. Remove K Digits

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn remove_kdigits(num: String, mut k: i32) -> String {
    let mut stack: Vec<char> = Vec::new();
    for c in num.chars() {
        while k > 0 && !stack.is_empty() && *stack.last().unwrap() > c {
            stack.pop();
            k -= 1;
        }
        stack.push(c);
    }
    while k > 0 && !stack.is_empty() {
        stack.pop();
        k -= 1;
    }
    let res: String = stack.into_iter().skip_while(|&c| c == '0').collect();
    if res.is_empty() { "0".to_string() } else { res }
}
```

## TypeScript Implementation
```typescript
export function removeKdigits(num: string, k: number): string {
    const stack: string[] = [];
    for (const c of num) {
        while (k > 0 && stack.length > 0 && stack[stack.length - 1] > c) {
            stack.pop();
            k--;
        }
        stack.push(c);
    }
    while (k > 0) {
        stack.pop();
        k--;
    }
    let start = 0;
    while (start < stack.length && stack[start] === '0') start++;
    const res = stack.slice(start).join('');
    return res.length === 0 ? '0' : res;
}
```
