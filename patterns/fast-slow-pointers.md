# Fast and Slow Pointers Pattern

## Concept
Also known as Floyd's Tortoise and Hare algorithm. Uses two pointers moving at different speeds (typically 1 step vs 2 steps) to detect cycles, identify middle nodes, or find entrance points in linked structures with O(1) space.

## TypeScript Implementation

```typescript
interface ListNode {
  val: number;
  next: ListNode | null;
}

export function hasCycle(head: ListNode | null): boolean {
  if (!head || !head.next) return false;

  let slow: ListNode | null = head;
  let fast: ListNode | null = head;

  while (fast !== null && fast.next !== null) {
    slow = slow!.next;
    fast = fast.next.next;

    if (slow === fast) {
      return true;
    }
  }

  return false;
}
```

## Rust Implementation

```rust
pub fn has_cycle_indices(arr: &[usize]) -> bool {
    if arr.is_empty() {
        return false;
    }

    let mut slow = 0;
    let mut fast = 0;

    loop {
        if fast >= arr.len() || arr[fast] >= arr.len() {
            return false;
        }

        slow = arr[slow];
        fast = arr[arr[fast]];

        if slow == fast {
            return true;
        }
    }
}
```

## Complexity Analysis
* **Time Complexity:** O(N) where N is the number of nodes/indices.
* **Space Complexity:** O(1) auxiliary space (zero dynamic allocation).
