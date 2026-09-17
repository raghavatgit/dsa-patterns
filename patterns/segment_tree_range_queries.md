# Pattern: Segment Tree with Lazy Propagation

## Overview
A Segment Tree is a binary tree data structure used for storing intervals or segments. It allows querying which of the stored segments contain a given point or performing range queries (such as sum, min, max, gcd) and range updates in $O(\log N)$ time.

## Lazy Propagation Mechanism
When updating a range `[L, R]`, updating every leaf node individually takes $O(N)$. Lazy propagation defers updates:
1. When a tree node's segment `[start, end]` falls completely within update query `[L, R]`, update the node's aggregate value and flag pending updates in a `lazy` array.
2. Return immediately without updating children.
3. When subsequent queries or updates visit this node, push pending lazy updates down to left and right children before recursing.
4. Ensures range queries and range updates execute in strict $O(\log N)$ time.

## Rust Implementation

```rust
pub struct SegmentTree {
    n: usize,
    tree: Vec<i64>,
    lazy: Vec<i64>,
}

impl SegmentTree {
    pub fn new(arr: &[i64]) -> Self {
        let n = arr.len();
        let mut st = Self {
            n,
            tree: vec![0; 4 * n],
            lazy: vec![0; 4 * n],
        };
        if n > 0 {
            st.build(arr, 0, 0, n - 1);
        }
        st
    }

    fn build(&mut self, arr: &[i64], node: usize, start: usize, end: usize) {
        if start == end {
            self.tree[node] = arr[start];
            return;
        }
        let mid = start + (end - start) / 2;
        let left = 2 * node + 1;
        let right = 2 * node + 2;

        self.build(arr, left, start, mid);
        self.build(arr, right, mid + 1, end);
        self.tree[node] = self.tree[left] + self.tree[right];
    }

    fn push_down(&mut self, node: usize, start: usize, end: usize) {
        if self.lazy[node] != 0 {
            let mid = start + (end - start) / 2;
            let left = 2 * node + 1;
            let right = 2 * node + 2;
            let val = self.lazy[node];

            self.tree[left] += val * (mid - start + 1) as i64;
            self.lazy[left] += val;

            self.tree[right] += val * (end - mid) as i64;
            self.lazy[right] += val;

            self.lazy[node] = 0;
        }
    }

    pub fn update_range(&mut self, l: usize, r: usize, delta: i64) {
        self.update_range_rec(0, 0, self.n - 1, l, r, delta);
    }

    fn update_range_rec(&mut self, node: usize, start: usize, end: usize, l: usize, r: usize, delta: i64) {
        if l <= start && end <= r {
            self.tree[node] += delta * (end - start + 1) as i64;
            self.lazy[node] += delta;
            return;
        }

        self.push_down(node, start, end);
        let mid = start + (end - start) / 2;
        let left = 2 * node + 1;
        let right = 2 * node + 2;

        if l <= mid {
            self.update_range_rec(left, start, mid, l, r, delta);
        }
        if r > mid {
            self.update_range_rec(right, mid + 1, end, l, r, delta);
        }

        self.tree[node] = self.tree[left] + self.tree[right];
    }

    pub fn query_range(&mut self, l: usize, r: usize) -> i64 {
        self.query_range_rec(0, 0, self.n - 1, l, r)
    }

    fn query_range_rec(&mut self, node: usize, start: usize, end: usize, l: usize, r: usize) -> i64 {
        if l <= start && end <= r {
            return self.tree[node];
        }

        self.push_down(node, start, end);
        let mid = start + (end - start) / 2;
        let left = 2 * node + 1;
        let right = 2 * node + 2;
        let mut sum = 0;

        if l <= mid {
            sum += self.query_range_rec(left, start, mid, l, r);
        }
        if r > mid {
            sum += self.query_range_rec(right, mid + 1, end, l, r);
        }

        sum
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_segment_tree_lazy() {
        let arr = vec![1, 2, 3, 4, 5];
        let mut st = SegmentTree::new(&arr);

        assert_eq!(st.query_range(0, 4), 15);
        assert_eq!(st.query_range(1, 3), 9);

        st.update_range(1, 3, 10); // arr becomes [1, 12, 13, 14, 5]
        assert_eq!(st.query_range(1, 3), 39);
        assert_eq!(st.query_range(0, 4), 45);
    }
}
```
