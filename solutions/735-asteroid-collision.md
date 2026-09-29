# 735. Asteroid Collision

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn asteroid_collision(asteroids: Vec<i32>) -> Vec<i32> {
    let mut stack: Vec<i32> = Vec::new();
    for &ast in &asteroids {
        let mut alive = true;
        while alive && ast < 0 && !stack.is_empty() && *stack.last().unwrap() > 0 {
            let top = *stack.last().unwrap();
            if top < -ast {
                stack.pop();
            } else if top == -ast {
                stack.pop();
                alive = false;
            } else {
                alive = false;
            }
        }
        if alive {
            stack.push(ast);
        }
    }
    stack
}
```

## TypeScript Implementation
```typescript
export function asteroidCollision(asteroids: number[]): number[] {
    const stack: number[] = [];
    for (const ast of asteroids) {
        let alive = true;
        while (alive && ast < 0 && stack.length > 0 && stack[stack.length - 1] > 0) {
            const top = stack[stack.length - 1];
            if (top < -ast) {
                stack.pop();
            } else if (top === -ast) {
                stack.pop();
                alive = false;
            } else {
                alive = false;
            }
        }
        if (alive) {
            stack.push(ast);
        }
    }
    return stack;
}
```
