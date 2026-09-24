# Problem 322: Coin Change

## Problem Statement
You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money. Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

## DP Recurrence
$$dp[a] = \min_{c \in coins}(dp[a - c] + 1) \quad \text{for } a \ge c$$
Base case: $dp[0] = 0$, all other amounts initialized to $\infty$.

## Complexity
- Time: $O(\text{amount} \times |coins|)$
- Space: $O(\text{amount})$

## C++ Implementation
```cpp
#include <vector>
#include <algorithm>

int coinChange(const std::vector<int>& coins, int amount) {
    const int INF = amount + 1;
    std::vector<int> dp(amount + 1, INF);
    dp[0] = 0;

    for (int a = 1; a <= amount; ++a) {
        for (int coin : coins) {
            if (a >= coin && dp[a - coin] != INF) {
                dp[a] = std::min(dp[a], dp[a - coin] + 1);
            }
        }
    }
    return dp[amount] > amount ? -1 : dp[amount];
}
```
