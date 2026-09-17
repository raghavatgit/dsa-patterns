# Patience Sorting and Greedy Binary Search Pattern

## Concept
Patience sorting is a card-sorting algorithm inspired by the card game Patience. It provides the theoretical foundation for computing the Longest Increasing Subsequence (LIS) in $O(N \log N)$ time.

Piles are formed according to two rules:
1. A card can be placed on an existing pile if and only if its value is less than or equal to the pile's top card.
2. If no existing pile can accept the card, create a new pile to the right of all existing piles.
3. Use binary search over pile top values to find the leftmost valid pile in $O(\log P)$ time.

The minimum number of piles required to sort the array equals the length of the Longest Increasing Subsequence.
