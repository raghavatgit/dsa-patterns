# 85. Maximal Rectangle

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(n)

## TypeScript Implementation
```typescript
export function maximalRectangle(matrix: string[][]): number {
    if (matrix.length === 0) return 0;
    const n = matrix[0].length;
    const heights = new Array(n).fill(0);
    let maxArea = 0;

    for (const row of matrix) {
        for (let j = 0; j < n; j++) {
            heights[j] = row[j] === '1' ? heights[j] + 1 : 0;
        }
        maxArea = Math.max(maxArea, largestRectangleArea(heights));
    }

    return maxArea;
}
```
