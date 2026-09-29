# 853. Car Fleet

## Complexity
- Time Complexity: O(n log n)
- Space Complexity: O(n)

## TypeScript Implementation
```typescript
export function carFleet(target: number, position: number[], speed: number[]): number {
    const cars = position.map((pos, idx) => ({ pos, time: (target - pos) / speed[idx] }));
    cars.sort((a, b) => b.pos - a.pos);

    let fleets = 0;
    let maxTime = 0;

    for (const car of cars) {
        if (car.time > maxTime) {
            fleets++;
            maxTime = car.time;
        }
    }

    return fleets;
}
```
