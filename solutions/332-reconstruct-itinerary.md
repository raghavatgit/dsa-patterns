# 332. Reconstruct Itinerary

## Problem Statement
You are given a list of airline tickets where `tickets[i] = [fromi, toi]` represent the departure and the arrival airports of one flight. Reconstruct the itinerary in order and return it.

All of the tickets belong to a man who departs from `"JFK"`, thus, the itinerary must begin with `"JFK"`. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string.

---

## TypeScript Implementation

```typescript
export function findItinerary(tickets: string[][]): string[] {
  const adj = new Map<string, string[]>();

  // Sort in reverse lexicographical order for efficient O(1) pop
  tickets.sort((a, b) => b[1].localeCompare(a[1]));

  for (const [from, to] of tickets) {
    if (!adj.has(from)) adj.set(from, []);
    adj.get(from)!.push(to);
  }

  const route: string[] = [];

  function dfs(airport: string): void {
    const destinations = adj.get(airport);
    while (destinations && destinations.length > 0) {
      const nextAirport = destinations.pop()!;
      dfs(nextAirport);
    }
    route.push(airport);
  }

  dfs("JFK");
  return route.reverse();
}
```

---

## Rust Implementation

```rust
use std::collections::{BinaryHeap, HashMap};
use std::cmp::Reverse;

pub struct Solution;

impl Solution {
    pub fn find_itinerary(tickets: Vec<Vec<String>>) -> Vec<String> {
        let mut adj: HashMap<String, BinaryHeap<Reverse<String>>> = HashMap::new();

        for ticket in tickets {
            let from = ticket[0].clone();
            let to = ticket[1].clone();
            adj.entry(from).or_default().push(Reverse(to));
        }

        let mut route = Vec::new();
        Self::dfs(&mut adj, "JFK".to_string(), &mut route);
        route.reverse();
        route
    }

    fn dfs(
        adj: &mut HashMap<String, BinaryHeap<Reverse<String>>>,
        airport: String,
        route: &mut Vec<String>,
    ) {
        while let Some(Reverse(next_airport)) = adj.get_mut(&airport).and_then(|h| h.pop()) {
            Self::dfs(adj, next_airport, route);
        }
        route.push(airport);
    }
}
```

---

## Complexity Analysis

- Time Complexity: `O(E log E)` where `E` is the number of tickets, due to heap sorting of destination vertices. Hierholzer's traversal runs in linear `O(E)` time.
- Space Complexity: `O(V + E)` for graph adjacency storage and recursion stack.
