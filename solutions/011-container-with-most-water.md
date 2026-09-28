# 11. Container With Most Water

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## TypeScript Implementation
```typescript
export function maxArea(height: number[]): number {
    let left = 0, right = height.length - 1, maxCapacity = 0;
    while (left < right) {
        const h = Math.min(height[left], height[right]);
        maxCapacity = Math.max(maxCapacity, h * (right - left));
        if (height[left] < height[right]) left++;
        else right--;
    }
    return maxCapacity;
}
```
