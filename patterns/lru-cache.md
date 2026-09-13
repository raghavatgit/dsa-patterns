# Least Recently Used (LRU) Cache

## Concept
An LRU cache evicts the item that has not been accessed for the longest duration when reaching maximum capacity. Achieving strict O(1) time complexity for both `get` and `put` operations requires combining two core structures:
1. **Hash Map:** Provides O(1) key-to-node lookup.
2. **Doubly Linked List:** Maintains recency ordering with O(1) node deletion and insertion at the head.

## TypeScript Implementation

```typescript
class DLinkedNode {
  key: number;
  val: number;
  prev: DLinkedNode | null = null;
  next: DLinkedNode | null = null;

  constructor(key: number = 0, val: number = 0) {
    this.key = key;
    this.val = val;
  }
}

export class LRUCache {
  private capacity: number;
  private map: Map<number, DLinkedNode> = new Map();
  private head: DLinkedNode = new DLinkedNode();
  private tail: DLinkedNode = new DLinkedNode();

  constructor(capacity: number) {
    this.capacity = capacity;
    this.head.next = this.tail;
    this.tail.prev = this.head;
  }

  get(key: number): number {
    const node = this.map.get(key);
    if (!node) return -1;

    this.moveToHead(node);
    return node.val;
  }

  put(key: number, value: number): void {
    const existing = this.map.get(key);
    if (existing) {
      existing.val = value;
      this.moveToHead(existing);
      return;
    }

    const newNode = new DLinkedNode(key, value);
    this.map.set(key, newNode);
    this.addNode(newNode);

    if (this.map.size > this.capacity) {
      const lru = this.popTail();
      this.map.delete(lru.key);
    }
  }

  private addNode(node: DLinkedNode): void {
    node.prev = this.head;
    node.next = this.head.next;
    this.head.next!.prev = node;
    this.head.next = node;
  }

  private removeNode(node: DLinkedNode): void {
    node.prev!.next = node.next;
    node.next!.prev = node.prev;
  }

  private moveToHead(node: DLinkedNode): void {
    this.removeNode(node);
    this.addNode(node);
  }

  private popTail(): DLinkedNode {
    const res = this.tail.prev!;
    this.removeNode(res);
    return res;
  }
}
```

## Complexity Analysis
* **Get Time:** O(1) hash lookup + list repositioning.
* **Put Time:** O(1) hash insertion + list insertion/eviction.
* **Space Complexity:** O(Capacity) auxiliary space for map entries and linked list nodes.
