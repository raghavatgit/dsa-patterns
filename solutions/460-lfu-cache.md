# 460. LFU Cache

## Complexity
- Time Complexity: O(1) get and put
- Space Complexity: O(capacity)

## TypeScript Implementation
```typescript
export class LFUCache {
    private capacity: number;
    private minFreq = 0;
    private keyMap = new Map<number, { val: number; freq: number }>();
    private freqMap = new Map<number, Set<number>>();

    constructor(capacity: number) {
        this.capacity = capacity;
    }

    get(key: number): number {
        if (!this.keyMap.has(key)) return -1;
        const item = this.keyMap.get(key)!;
        this.updateFreq(key, item);
        return item.val;
    }

    put(key: number, value: number): void {
        if (this.capacity === 0) return;
        if (this.keyMap.has(key)) {
            const item = this.keyMap.get(key)!;
            item.val = value;
            this.updateFreq(key, item);
        } else {
            if (this.keyMap.size >= this.capacity) {
                const evictSet = this.freqMap.get(this.minFreq)!;
                const evictKey = evictSet.keys().next().value;
                evictSet.delete(evictKey);
                this.keyMap.delete(evictKey);
            }
            this.keyMap.set(key, { val: value, freq: 1 });
            if (!this.freqMap.has(1)) this.freqMap.set(1, new Set());
            this.freqMap.get(1)!.add(key);
            this.minFreq = 1;
        }
    }

    private updateFreq(key: number, item: { val: number; freq: number }) {
        const oldSet = this.freqMap.get(item.freq)!;
        oldSet.delete(key);
        if (oldSet.size === 0 && item.freq === this.minFreq) this.minFreq++;
        item.freq++;
        if (!this.freqMap.has(item.freq)) this.freqMap.set(item.freq, new Set());
        this.freqMap.get(item.freq)!.add(key);
    }
}
```
