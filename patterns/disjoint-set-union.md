# Disjoint Set Union (Union-Find) Pattern

## Concept
Disjoint Set Union (DSU) maintains a partition of a set into disjoint connected subsets. It efficiently answers two questions:
1. **`find(x)`:** Which subset does element `x` belong to?
2. **`union(x, y)`:** Merge the subset containing `x` with the subset containing `y`.

Using **Path Compression** (flattening the tree during `find`) and **Union by Rank** (attaching smaller trees under larger trees), operation complexity drops to $O(lpha(N))$ amortized time, where $lpha$ is the nearly constant Inverse Ackermann function.

## TypeScript Implementation

```typescript
export class DisjointSetUnion {
  private parent: number[];
  private rank: number[];
  private count: number;

  constructor(size: number) {
    this.count = size;
    this.parent = new Array(size);
    this.rank = new Array(size).fill(0);
    for (let i = 0; i < size; i++) {
      this.parent[i] = i;
    }
  }

  find(x: number): number {
    if (this.parent[x] !== x) {
      // Path compression: points node directly to representative root
      this.parent[x] = this.find(this.parent[x]);
    }
    return this.parent[x];
  }

  union(x: number, y: number): boolean {
    const rootX = this.find(x);
    const rootY = this.find(y);

    if (rootX === rootY) {
      return false; // Cycle detected: already in same connected component
    }

    // Union by rank: attach smaller depth tree to larger depth root
    if (this.rank[rootX] < this.rank[rootY]) {
      this.parent[rootX] = rootY;
    } else if (this.rank[rootX] > this.rank[rootY]) {
      this.parent[rootY] = rootX;
    } else {
      this.parent[rootY] = rootX;
      this.rank[rootX]++;
    }

    this.count--;
    return true;
  }

  getComponentCount(): number {
    return this.count;
  }
}
```

## Rust Implementation

```rust
pub struct DisjointSetUnion {
    parent: Vec<usize>,
    rank: Vec<usize>,
    count: usize,
}

impl DisjointSetUnion {
    pub fn new(size: usize) -> Self {
        DisjointSetUnion {
            parent: (0..size).collect(),
            rank: vec![0; size],
            count: size,
        }
    }

    pub fn find(&mut self, x: usize) -> usize {
        if self.parent[x] != x {
            let root = self.find(self.parent[x]);
            self.parent[x] = root; // Path compression
        }
        self.parent[x]
    }

    pub fn union(&mut self, x: usize, y: usize) -> bool {
        let root_x = self.find(x);
        let root_y = self.find(y);

        if root_x == root_y {
            return false;
        }

        if self.rank[root_x] < self.rank[root_y] {
            self.parent[root_x] = root_y;
        } else if self.rank[root_x] > self.rank[root_y] {
            self.parent[root_y] = root_x;
        } else {
            self.parent[root_y] = root_x;
            self.rank[root_x] += 1;
        }

        self.count -= 1;
        true
    }

    pub fn component_count(&self) -> usize {
        self.count
    }
}
```

## Complexity Analysis
* **Time Complexity:** O(alpha(N)) amortized per operation (practically <= 4 for all realistic N).
* **Space Complexity:** O(N) auxiliary space for parent and rank arrays.
