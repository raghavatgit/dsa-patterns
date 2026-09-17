# Problem: LRU Cache (Doubly Linked List + HashMap)

## Problem Statement
Design a data structure that follows the constraints of a Least Recently Used (LRU) cache. Implement `get(key)` and `put(key, value)` with average $O(1)$ time complexity.

## Intuition & Approach
1. Use a doubly linked list with dummy head and tail sentinel nodes.
2. The most recently accessed node resides directly before the dummy tail; least recently used node resides after the dummy head.
3. A hash map stores keys mapped to linked list node references for $O(1)$ node lookup.
4. On `get(key)`: If present, remove node from current position and append before dummy tail; return value.
5. On `put(key, value)`: If key exists, update value and move to tail. If new key, insert node before tail. If capacity exceeded, evict node after dummy head and remove from map.

## TypeScript Implementation

```typescript
class DNode {
  key: number;
  val: number;
  prev: DNode | null = null;
  next: DNode | null = null;
  constructor(key: number = 0, val: number = 0) {
    this.key = key;
    this.val = val;
  }
}

export class LRUCache {
  private capacity: number;
  private map: Map<number, DNode> = new Map();
  private head: DNode = new DNode();
  private tail: DNode = new DNode();

  constructor(capacity: number) {
    this.capacity = capacity;
    this.head.next = this.tail;
    this.tail.prev = this.head;
  }

  private remove(node: DNode): void {
    node.prev!.next = node.next;
    node.next!.prev = node.prev;
  }

  private append(node: DNode): void {
    node.prev = this.tail.prev;
    node.next = this.tail;
    this.tail.prev!.next = node;
    this.tail.prev = node;
  }

  get(key: number): number {
    const node = this.map.get(key);
    if (!node) return -1;
    this.remove(node);
    this.append(node);
    return node.val;
  }

  put(key: number, value: number): void {
    if (this.map.has(key)) {
      const node = this.map.get(key)!;
      node.val = value;
      this.remove(node);
      this.append(node);
    } else {
      if (this.map.size >= this.capacity) {
        const lru = this.head.next!;
        this.remove(lru);
        this.map.delete(lru.key);
      }
      const newNode = new DNode(key, value);
      this.map.set(key, newNode);
      this.append(newNode);
    }
  }
}
```
