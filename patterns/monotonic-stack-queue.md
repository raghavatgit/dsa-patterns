# Pattern: Monotonic Stack and Deque

## Core Concept
A monotonic stack maintains elements in strictly increasing or strictly decreasing order.
When an incoming element violates the monotonic property, elements are popped from the stack.
The act of popping reveals:
1. The next smaller/greater element (the incoming element triggering the pop).
2. The previous smaller/greater element (the new top of the stack after popping).

## Canonical Problems
- Next Greater Element (Circular or Linear)
- Daily Temperatures
- Largest Rectangle in Histogram
- Maximal Rectangle
- Sliding Window Maximum (Monotonic Deque)
- Online Stock Span

## Summary Table of Bounds
| Problem | Structure | Time | Space |
| :--- | :--- | :--- | :--- |
| Daily Temperatures | Decreasing Stack | $O(N)$ | $O(N)$ |
| Largest Rectangle | Increasing Stack | $O(N)$ | $O(N)$ |
| Sliding Window Max | Decreasing Deque | $O(N)$ | $O(K)$ |
