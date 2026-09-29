# 455. Assign Cookies

## Complexity
- Time Complexity: O(n log n + m log m)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn find_content_children(mut g: Vec<i32>, mut s: Vec<i32>) -> i32 {
    g.sort();
    s.sort();
    let mut child = 0;
    let mut cookie = 0;
    while child < g.len() && cookie < s.len() {
        if s[cookie] >= g[child] {
            child += 1;
        }
        cookie += 1;
    }
    child as i32
}
```

## TypeScript Implementation
```typescript
export function findContentChildren(g: number[], s: number[]): number {
    g.sort((a, b) => a - b);
    s.sort((a, b) => a - b);
    let child = 0, cookie = 0;
    while (child < g.length && cookie < s.length) {
        if (s[cookie] >= g[child]) {
            child++;
        }
        cookie++;
    }
    return child;
}
```
