# 225. Implement Stack using Queues

## Problem Statement
Implement a last-in-first-out (LIFO) stack using only standard FIFO queue operations.

---

## TypeScript Implementation

```typescript
export class MyStack {
  private queue: number[] = [];

  push(x: number): void {
    this.queue.push(x);
    for (let i = 0; i < this.queue.length - 1; i++) {
      this.queue.push(this.queue.shift()!);
    }
  }

  pop(): number {
    return this.queue.shift()!;
  }

  top(): number {
    return this.queue[0];
  }

  empty(): boolean {
    return this.queue.length === 0;
  }
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) push, O(1) pop.
* **Space Complexity:** O(N).
