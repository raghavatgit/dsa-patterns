# 150. Evaluate Reverse Polish Notation

## Problem Statement
Evaluate the value of an arithmetic expression in Reverse Polish Notation (RPN / Postfix). Valid operators are `+`, `-`, `*`, and `/`. Each operand may be an integer or another expression. Division between two integers truncates toward zero.

---

## Stack Evaluation Invariants

In Postfix notation, operands appear before their operator. A LIFO stack stores operands until an operator is encountered, popping the right operand followed by the left operand.

---

## TypeScript Implementation

```typescript
export function evalRPN(tokens: string[]): number {
  const stack: number[] = [];

  for (const token of tokens) {
    if (token === '+' || token === '-' || token === '*' || token === '/') {
      const b = stack.pop()!;
      const a = stack.pop()!;
      
      switch (token) {
        case '+':
          stack.push(a + b);
          break;
        case '-':
          stack.push(a - b);
          break;
        case '*':
          stack.push(a * b);
          break;
        case '/':
          // Truncate towards zero matching integer division
          stack.push(Math.trunc(a / b));
          break;
      }
    } else {
      stack.push(parseInt(token, 10));
    }
  }

  return stack[0];
}
```

---

## Rust Implementation

```rust
pub fn eval_rpn(tokens: Vec<String>) -> i32 {
    let mut stack: Vec<i32> = Vec::with_capacity(tokens.len());

    for token in tokens {
        match token.as_str() {
            "+" => {
                let b = stack.pop().unwrap();
                let a = stack.pop().unwrap();
                stack.push(a + b);
            }
            "-" => {
                let b = stack.pop().unwrap();
                let a = stack.pop().unwrap();
                stack.push(a - b);
            }
            "*" => {
                let b = stack.pop().unwrap();
                let a = stack.pop().unwrap();
                stack.push(a * b);
            }
            "/" => {
                let b = stack.pop().unwrap();
                let a = stack.pop().unwrap();
                stack.push(a / b);
            }
            val => {
                stack.push(val.parse::<i32>().unwrap());
            }
        }
    }

    stack.pop().unwrap()
}
```

---

## Complexity Analysis

* **Time Complexity:** `O(N)` where `N` is the number of tokens. Every token is processed once with constant time stack operations.
* **Space Complexity:** `O(N)` in the worst case to store numeric operands on the stack.
