# 232. Implement Queue using Stacks

## Problem Statement
Implement a first in first out (FIFO) queue using only two LIFO stacks.

---

## Amortized O(1) Push/Pop
Input stack receives pushes. Output stack handles pops/peeks. Shift elements from input to output only when output stack is empty.

---

## TypeScript Implementation

```typescript
export class MyQueue {
  private inStack: number[] = [];
  private outStack: number[] = [];

  push(x: number): void {
    this.inStack.push(x);
  }

  pop(): number {
    this.shift();
    return this.outStack.pop()!;
  }

  peek(): number {
    this.shift();
    return this.outStack[this.outStack.length - 1];
  }

  empty(): boolean {
    return this.inStack.length === 0 && this.outStack.length === 0;
  }

  private shift(): void {
    if (this.outStack.length === 0) {
      while (this.inStack.length > 0) {
        this.outStack.push(this.inStack.pop()!);
      }
    }
  }
}
```

---

## Complexity Analysis
* **Time Complexity:** Amortized O(1) for all operations.
* **Space Complexity:** O(N).
