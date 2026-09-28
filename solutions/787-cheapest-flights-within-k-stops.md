# 787. Cheapest Flights Within K Stops

## Complexity
- Time Complexity: O(K * E)
- Space Complexity: O(V)

## TypeScript Implementation
```typescript
export function findCheapestPrice(n: number, flights: number[][], src: number, dst: number, k: number): number {
    let prices = new Array(n).fill(Infinity);
    prices[src] = 0;

    for (let i = 0; i <= k; i++) {
        const temp = [...prices];
        for (const [from, to, cost] of flights) {
            if (prices[from] === Infinity) continue;
            if (prices[from] + cost < temp[to]) {
                temp[to] = prices[from] + cost;
            }
        }
        prices = temp;
    }

    return prices[dst] === Infinity ? -1 : prices[dst];
}
```
