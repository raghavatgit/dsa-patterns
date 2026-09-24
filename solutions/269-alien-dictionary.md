# Problem 269: Alien Dictionary

## Problem Statement
Given a sorted list of words in an alien language, derive the order of letters in the language.

## Edge Cases and Rules
1. Compare adjacent words $w_1$ and $w_2$.
2. The first differing character defines directed edge $w_1[k] \to w_2[k]$.
3. If $w_2$ is a prefix of $w_1$ and $|w_1| > |w_2|$, order is invalid (e.g. `["abc", "ab"]`). Return `""`.
4. Apply Kahn's algorithm or Tarjan's DFS on extracted DAG.

## Complexity
- Time: $O(C)$ where $C$ is total characters across all words.
- Space: $O(U + E)$ where $U \le 26$.

## C++ Implementation
```cpp
#include <string>
#include <vector>
#include <unordered_map>
#include <unordered_set>
#include <queue>

std::string alienOrder(const std::vector<std::string>& words) {
    std::unordered_map<char, std::unordered_set<char>> adj;
    std::unordered_map<char, int> in_degree;

    for (const auto& w : words) {
        for (char c : w) {
            in_degree[c] = 0;
        }
    }

    for (size_t i = 0; i < words.size() - 1; ++i) {
        const std::string& w1 = words[i];
        const std::string& w2 = words[i + 1];
        size_t len = std::min(w1.length(), w2.length());
        bool diff_found = false;

        for (size_t j = 0; j < len; ++j) {
            if (w1[j] != w2[j]) {
                if (!adj[w1[j]].count(w2[j])) {
                    adj[w1[j]].insert(w2[j]);
                    in_degree[w2[j]]++;
                }
                diff_found = true;
                break;
            }
        }

        if (!diff_found && w1.length() > w2.length()) {
            return ""; // Invalid prefix order
        }
    }

    std::queue<char> q;
    for (const auto& [c, deg] : in_degree) {
        if (deg == 0) q.push(c);
    }

    std::string order;
    while (!q.empty()) {
        char u = q.front();
        q.pop();
        order += u;

        for (char v : adj[u]) {
            if (--in_degree[v] == 0) {
                q.push(v);
            }
        }
    }

    return order.length() == in_degree.size() ? order : "";
}
```
