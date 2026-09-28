# 295. Find Median from Data Stream

## Complexity
- addNum: O(log n)
- findMedian: O(1)
- Space Complexity: O(n)

## TypeScript Implementation
```typescript
export class MedianFinder {
    private small: number[] = []; // max heap
    private large: number[] = []; // min heap

    addNum(num: number): void {
        this.small.push(num);
        this.small.sort((a, b) => b - a);
        this.large.push(this.small.shift()!);
        this.large.sort((a, b) => a - b);

        if (this.large.length > this.small.length) {
            this.small.push(this.large.shift()!);
            this.small.sort((a, b) => b - a);
        }
    }

    findMedian(): number {
        if (this.small.length > this.large.length) return this.small[0];
        return (this.small[0] + this.large[0]) / 2;
    }
}
```
