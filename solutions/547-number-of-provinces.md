# 547. Number of Provinces

## Problem Statement
There are `n` cities. Some are connected directly while some are connected indirectly. A province is a group of directly or indirectly connected cities. Return the total number of provinces given an adjacency matrix `is_connected`.

---

## Method Explanation
Union-Find / Disjoint Set Union (DSU):
- Initialize `n` disjoint sets with rank.
- For each edge `is_connected[i][j] == 1`, union sets `i` and `j`.
- Decrement count of disjoint components on successful union.

---

## Rust Implementation

```rust
pub struct Solution;

struct Dsu {
    parent: Vec<usize>,
    rank: Vec<usize>,
    count: usize,
}

impl Dsu {
    fn new(n: usize) -> Self {
        Self {
            parent: (0..n).collect(),
            rank: vec![0; n],
            count: n,
        }
    }

    fn find(&mut self, i: usize) -> usize {
        if self.parent[i] != i {
            self.parent[i] = self.find(self.parent[i]);
        }
        self.parent[i]
    }

    fn union(&mut self, i: usize, j: usize) -> bool {
        let root_i = self.find(i);
        let root_j = self.find(j);
        if root_i == root_j {
            return false;
        }

        if self.rank[root_i] < self.rank[root_j] {
            self.parent[root_i] = root_j;
        } else if self.rank[root_i] > self.rank[root_j] {
            self.parent[root_j] = root_i;
        } else {
            self.parent[root_j] = root_i;
            self.rank[root_i] += 1;
        }

        self.count -= 1;
        true
    }
}

impl Solution {
    pub fn find_circle_num(is_connected: Vec<Vec<i32>>) -> i32 {
        let n = is_connected.len();
        let mut dsu = Dsu::new(n);

        for i in 0..n {
            for j in (i + 1)..n {
                if is_connected[i][j] == 1 {
                    dsu.union(i, j);
                }
            }
        }

        dsu.count as i32
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_provinces() {
        assert_eq!(
            Solution::find_circle_num(vec![
                vec![1, 1, 0],
                vec![1, 1, 0],
                vec![0, 0, 1]
            ]),
            2
        );
    }
}
```

---

## Complexity Analysis
- Time Complexity: `O(N^2 * alpha(N))` where `alpha` is the inverse Ackermann function.
- Space Complexity: `O(N)` for parent and rank arrays.
