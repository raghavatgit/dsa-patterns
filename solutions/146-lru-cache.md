# 146. LRU Cache

## Complexity
- Time Complexity: O(1) get and put
- Space Complexity: O(capacity)

## TypeScript Implementation
```typescript
class DLinkedNode {
    key: number; val: number;
    prev: DLinkedNode | null = null;
    next: DLinkedNode | null = null;
    constructor(k = 0, v = 0) { this.key = k; this.val = v; }
}

export class LRUCache {
    private capacity: number;
    private map = new Map<number, DLinkedNode>();
    private head = new DLinkedNode();
    private tail = new DLinkedNode();

    constructor(capacity: number) {
        this.capacity = capacity;
        this.head.next = this.tail;
        this.tail.prev = this.head;
    }

    get(key: number): number {
        if (!this.map.has(key)) return -1;
        const node = this.map.get(key)!;
        this.moveToHead(node);
        return node.val;
    }

    put(key: number, value: number): void {
        if (this.map.has(key)) {
            const node = this.map.get(key)!;
            node.val = value;
            this.moveToHead(node);
        } else {
            const newNode = new DLinkedNode(key, value);
            this.map.set(key, newNode);
            this.addNode(newNode);
            if (this.map.size > this.capacity) {
                const tailPrev = this.popTail();
                this.map.delete(tailPrev.key);
            }
        }
    }

    private addNode(node: DLinkedNode) {
        node.prev = this.head;
        node.next = this.head.next;
        this.head.next!.prev = node;
        this.head.next = node;
    }

    private removeNode(node: DLinkedNode) {
        node.prev!.next = node.next;
        node.next!.prev = node.prev;
    }

    private moveToHead(node: DLinkedNode) {
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
