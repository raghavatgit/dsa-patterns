# 981. Time Based Key-Value Store

## Problem Statement
Design a time-based key-value data structure that can store multiple values for the same key at different time stamps and retrieve the key's value at a certain timestamp.

Implement the `TimeMap` class:
- `TimeMap()` Initializes the object of the data structure.
- `void set(String key, String value, int timestamp)` Stores the key `key` with the value `value` at the given time `timestamp`.
- `String get(String key, int timestamp)` Returns a value such that `set` was called previously, with `timestamp_prev <= timestamp`. If there are multiple such values, it returns the value associated with the largest `timestamp_prev`. If there are no values, it returns `""`.

---

## TypeScript Implementation

```typescript
interface TimeEntry {
  timestamp: number;
  value: string;
}

export class TimeMap {
  private store: Map<string, TimeEntry[]>;

  constructor() {
    this.store = new Map();
  }

  set(key: string, value: string, timestamp: number): void {
    if (!this.store.has(key)) {
      this.store.set(key, []);
    }
    this.store.get(key)!.push({ timestamp, value });
  }

  get(key: string, timestamp: number): string {
    const list = this.store.get(key);
    if (!list || list.length === 0) return "";

    let left = 0;
    let right = list.length - 1;
    let res = "";

    while (left <= right) {
      const mid = left + Math.floor((right - left) / 2);
      if (list[mid].timestamp <= timestamp) {
        res = list[mid].value;
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }

    return res;
  }
}
```

---

## Rust Implementation

```rust
use std::collections::HashMap;

pub struct TimeMap {
    store: HashMap<String, Vec<(i32, String)>>,
}

impl TimeMap {
    pub fn new() -> Self {
        Self {
            store: HashMap::new(),
        }
    }

    pub fn set(&mut self, key: String, value: String, timestamp: i32) {
        self.store.entry(key).or_default().push((timestamp, value));
    }

    pub fn get(&self, key: String, timestamp: i32) -> String {
        match self.store.get(&key) {
            None => String::new(),
            Some(entries) => {
                let mut left: usize = 0;
                if entries.is_empty() {
                    return String::new();
                }
                let mut right: usize = entries.len() - 1;
                let mut result_idx: Option<usize> = None;

                while left <= right {
                    let mid = left + (right - left) / 2;
                    if entries[mid].0 <= timestamp {
                        result_idx = Some(mid);
                        left = mid + 1;
                    } else {
                        if mid == 0 {
                            break;
                        }
                        right = mid - 1;
                    }
                }

                match result_idx {
                    Some(idx) => entries[idx].1.clone(),
                    None => String::new(),
                }
            }
        }
    }
}
```

---

## Complexity Analysis

- Time Complexity:
  - `set`: `O(1)` amortized append.
  - `get`: `O(log n)` binary search across sorted timestamps.
- Space Complexity: `O(n)` where `n` is the total number of key-value-timestamp entries.
