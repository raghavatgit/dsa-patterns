# 42. Trapping Rain Water

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## TypeScript Implementation
```typescript
export function trap(height: number[]): number {
    let left = 0, right = height.length - 1;
    let leftMax = 0, rightMax = 0, total = 0;

    while (left < right) {
        if (height[left] < height[right]) {
            if (height[left] >= leftMax) leftMax = height[left];
            else total += leftMax - height[left];
            left++;
        } else {
            if (height[right] >= rightMax) rightMax = height[right];
            else total += rightMax - height[right];
            right--;
        }
    }

    return total;
}
```
