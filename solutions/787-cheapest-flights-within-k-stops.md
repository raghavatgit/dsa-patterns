# Problem 787: Cheapest Flights Within K Stops

## Problem Statement
There are `n` cities connected by some number of flights. Find the cheapest price from `src` to `dst` with at most `k` stops. If there is no such route, return `-1`.

## Approach
Bellman-Ford Algorithm with $K + 1$ iterations:
To avoid using more than $k$ stops within the same iteration, use a snapshot array `prev_prices` from the previous step.

## Complexity
- Time: $O(K \times E)$
- Space: $O(V)$

## C++ Implementation
```cpp
#include <vector>
#include <algorithm>
#include <climits>

int findCheapestPrice(int n, const std::vector<std::vector<int>>& flights, int src, int dst, int k) {
    std::vector<int> prices(n, INT_MAX);
    prices[src] = 0;

    for (int i = 0; i <= k; ++i) {
        std::vector<int> temp = prices;
        for (const auto& f : flights) {
            int u = f[0], v = f[1], price = f[2];
            if (prices[u] != INT_MAX && prices[u] + price < temp[v]) {
                temp[v] = prices[u] + price;
            }
        }
        prices = std::move(temp);
    }

    return prices[dst] == INT_MAX ? -1 : prices[dst];
}
```
