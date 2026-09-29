# 57. Insert Interval

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## TypeScript Implementation
```typescript
export function insert(intervals: number[][], newInterval: number[]): number[][] {
    const res: number[][] = [];
    let i = 0;
    const n = intervals.length;

    while (i < n && intervals[i][1] < newInterval[0]) {
        res.push(intervals[i]);
        i++;
    }

    while (i < n && intervals[i][0] <= newInterval[1]) {
        newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
        newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
        i++;
    }
    res.push(newInterval);

    while (i < n) {
        res.push(intervals[i]);
        i++;
    }

    return res;
}
```
