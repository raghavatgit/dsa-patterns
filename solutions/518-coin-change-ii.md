# Problem 518: Coin Change II

## Problem Statement
You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money. Return the number of combinations that make up that amount.

## Combination Invariant
To count combinations (ordered unique sets) rather than permutations, iterate outer loop over coins and inner loop over amounts from `coin` to `amount`.

## Complexity
- Time: $O(|coins| \times \text{amount})$
- Space: $O(\text{amount})$

## C++ Implementation
```cpp
#include <vector>

int change(int amount, const std::vector<int>& coins) {
    std::vector<unsigned long long> dp(amount + 1, 0);
    dp[0] = 1;

    for (int coin : coins) {
        for (int a = coin; a <= amount; ++a) {
            dp[a] += dp[a - coin];
        }
    }
    return static_cast<int>(dp[amount]);
}
```
