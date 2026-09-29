# 304. Range Sum Query 2D - Immutable

## Complexity
- Time Complexity: O(1) query, O(m * n) preprocessing
- Space Complexity: O(m * n)

## Rust Implementation
```rust
pub struct NumMatrix {
    dp: Vec<Vec<i32>>,
}

impl NumMatrix {
    pub fn new(matrix: Vec<Vec<i32>>) -> Self {
        if matrix.is_empty() || matrix[0].is_empty() {
            return NumMatrix { dp: vec![] };
        }
        let m = matrix.len();
        let n = matrix[0].len();
        let mut dp = vec![vec![0; n + 1]; m + 1];
        for r in 0..m {
            for c in 0..n {
                dp[r + 1][c + 1] = matrix[r][c] + dp[r][c + 1] + dp[r + 1][c] - dp[r][c];
            }
        }
        NumMatrix { dp }
    }

    pub fn sum_region(&self, row1: i32, col1: i32, row2: i32, col2: i32) -> i32 {
        let r1 = row1 as usize;
        let c1 = col1 as usize;
        let r2 = row2 as usize + 1;
        let c2 = col2 as usize + 1;
        self.dp[r2][c2] - self.dp[r1][c2] - self.dp[r2][c1] + self.dp[r1][c1]
    }
}
```

## TypeScript Implementation
```typescript
export class NumMatrix {
    private dp: number[][];

    constructor(matrix: number[][]) {
        const m = matrix.length;
        const n = matrix[0].length;
        this.dp = Array.from({ length: m + 1 }, () => new Array(n + 1).fill(0));
        for (let r = 0; r < m; r++) {
            for (let c = 0; c < n; c++) {
                this.dp[r + 1][c + 1] = matrix[r][c] + this.dp[r][c + 1] + this.dp[r + 1][c] - this.dp[r][c];
            }
        }
    }

    sumRegion(row1: number, col1: number, row2: number, col2: number): number {
        return this.dp[row2 + 1][col2 + 1] - this.dp[row1][col2 + 1] - this.dp[row2 + 1][col1] + this.dp[row1][col1];
    }
}
```
