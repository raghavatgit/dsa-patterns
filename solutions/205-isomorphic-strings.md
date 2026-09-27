# 205. Isomorphic Strings

## Problem Statement
Given two strings `s` and `t`, determine if they are isomorphic (characters in `s` can be replaced to get `t` bijectively).

---

## TypeScript Implementation

```typescript
export function isIsomorphic(s: string, t: string): boolean {
  if (s.length !== t.length) return false;
  const m1 = new Array(256).fill(0);
  const m2 = new Array(256).fill(0);

  for (let i = 0; i < s.length; i++) {
    const c1 = s.charCodeAt(i);
    const c2 = t.charCodeAt(i);
    if (m1[c1] !== m2[c2]) return false;
    m1[c1] = i + 1;
    m2[c2] = i + 1;
  }

  return true;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N).
* **Space Complexity:** O(1) fixed 256 size ASCII arrays.
