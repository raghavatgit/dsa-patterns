# 028. Find the Index of the First Occurrence in a String

## Problem Statement
Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

---

## Knuth-Morris-Pratt (KMP) Algorithm
Precompute the Longest Prefix Suffix (LPS) array for `needle` in O(M) time. Match against `haystack` in O(N) time without backtracking the haystack pointer.

---

## TypeScript Implementation

```typescript
export function strStr(haystack: string, needle: string): number {
  if (needle.length === 0) return 0;
  const lps = computeLPS(needle);
  let i = 0, j = 0;

  while (i < haystack.length) {
    if (haystack[i] === needle[j]) {
      i++;
      j++;
    }

    if (j === needle.length) {
      return i - j;
    } else if (i < haystack.length && haystack[i] !== needle[j]) {
      if (j !== 0) {
        j = lps[j - 1];
      } else {
        i++;
      }
    }
  }

  return -1;
}

function computeLPS(pattern: string): number[] {
  const lps = new Array(pattern.length).fill(0);
  let len = 0, i = 1;

  while (i < pattern.length) {
    if (pattern[i] === pattern[len]) {
      len++;
      lps[i] = len;
      i++;
    } else {
      if (len !== 0) {
        len = lps[len - 1];
      } else {
        lps[i] = 0;
        i++;
      }
    }
  }
  return lps;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N + M) linear guarantee.
* **Space Complexity:** O(M) for LPS lookup table.
