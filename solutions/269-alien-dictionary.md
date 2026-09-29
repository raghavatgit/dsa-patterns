# 269. Alien Dictionary

## Complexity
- Time Complexity: O(C) total characters across words
- Space Complexity: O(1) fixed 26 alphabet nodes

## TypeScript Implementation
```typescript
export function alienOrder(words: string[]): string {
    const adj = new Map<string, Set<string>>();
    const inDegree = new Map<string, number>();

    for (const w of words) {
        for (const c of w) {
            inDegree.set(c, 0);
            adj.set(c, new Set());
        }
    }

    for (let i = 0; i < words.length - 1; i++) {
        const w1 = words[i], w2 = words[i + 1];
        if (w1.length > w2.length && w1.startsWith(w2)) return "";
        for (let j = 0; j < Math.min(w1.length, w2.length); j++) {
            if (w1[j] !== w2[j]) {
                if (!adj.get(w1[j])!.has(w2[j])) {
                    adj.get(w1[j])!.add(w2[j]);
                    inDegree.set(w2[j], inDegree.get(w2[j])! + 1);
                }
                break;
            }
        }
    }

    const queue: string[] = [];
    for (const [char, deg] of inDegree.entries()) {
        if (deg === 0) queue.push(char);
    }

    let result = "";
    while (queue.length > 0) {
        const char = queue.shift()!;
        result += char;
        for (const next of adj.get(char)!) {
            inDegree.set(next, inDegree.get(next)! - 1);
            if (inDegree.get(next) === 0) queue.push(next);
        }
    }

    return result.length === inDegree.size ? result : "";
}
```
