# 036. Valid Sudoku

## Problem Statement
Determine if a 9 x 9 Sudoku board is valid. Only filled cells need to be validated according to standard Sudoku rules:
1. Each row contains digits 1-9 without repetition.
2. Each column contains digits 1-9 without repetition.
3. Each 3 x 3 subgrid contains digits 1-9 without repetition.

---

## Bitmask Solution
Use 9 integers for rows, 9 for cols, and 9 for 3x3 boxes. Set the `(val - 1)`-th bit for each digit. If `(mask & (1 << digit)) > 0`, repetition occurs in O(1) bitwise operations.

---

## TypeScript Implementation

```typescript
export function isValidSudoku(board: string[][]): boolean {
  const rows = new Array(9).fill(0);
  const cols = new Array(9).fill(0);
  const boxes = new Array(9).fill(0);

  for (let r = 0; r < 9; r++) {
    for (let c = 0; c < 9; c++) {
      const ch = board[r][c];
      if (ch === '.') continue;

      const val = ch.charCodeAt(0) - 49; // 0 to 8
      const bit = 1 << val;
      const bIdx = Math.floor(r / 3) * 3 + Math.floor(c / 3);

      if ((rows[r] & bit) || (cols[c] & bit) || (boxes[bIdx] & bit)) {
        return false;
      }

      rows[r] |= bit;
      cols[c] |= bit;
      boxes[bIdx] |= bit;
    }
  }

  return true;
}
```

---

## Rust Implementation

```rust
pub fn is_valid_sudoku(board: Vec<Vec<char>>) -> bool {
    let mut rows = [0u16; 9];
    let mut cols = [0u16; 9];
    let mut boxes = [0u16; 9];

    for r in 0..9 {
        for c in 0..9 {
            let ch = board[r][c];
            if ch == '.' {
                continue;
            }

            let val = (ch as u8 - b'1') as usize;
            let bit = 1u16 << val;
            let b_idx = (r / 3) * 3 + (c / 3);

            if (rows[r] & bit) != 0 || (cols[c] & bit) != 0 || (boxes[b_idx] & bit) != 0 {
                return false;
            }

            rows[r] |= bit;
            cols[c] |= bit;
            boxes[b_idx] |= bit;
        }
    }

    true
}
```

---

## Complexity Analysis
* **Time Complexity:** O(81) = O(1) fixed grid size.
* **Space Complexity:** O(1) with 27 scalar bitmask integers.
