# Problem 127: Word Ladder

## Problem Statement
A transformation sequence from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that every adjacent pair of words differs by a single letter. Return the number of words in the shortest transformation sequence.

## Bidirectional BFS
Expand from both `beginSet` and `endSet`. Always pick the smaller set to expand to minimize branching factor.

## Complexity
- Time: $O(M^2 \times N)$ where $M$ is word length, $N$ is dictionary size.
- Space: $O(M \times N)$

## C++ Implementation
```cpp
#include <string>
#include <vector>
#include <unordered_set>

int ladderLength(std::string beginWord, std::string endWord, std::vector<std::string>& wordList) {
    std::unordered_set<std::string> dict(wordList.begin(), wordList.end());
    if (!dict.count(endWord)) return 0;

    std::unordered_set<std::string> begin_set = {beginWord};
    std::unordered_set<std::string> end_set = {endWord};
    int steps = 1;

    while (!begin_set.empty() && !end_set.empty()) {
        if (begin_set.size() > end_set.size()) {
            std::swap(begin_set, end_set);
        }

        std::unordered_set<std::string> next_set;
        for (std::string word : begin_set) {
            dict.erase(word);
        }

        for (std::string word : begin_set) {
            for (size_t i = 0; i < word.length(); ++i) {
                char orig = word[i];
                for (char c = 'a'; c <= 'z'; ++c) {
                    word[i] = c;
                    if (end_set.count(word)) return steps + 1;
                    if (dict.count(word)) {
                        next_set.insert(word);
                        dict.erase(word);
                    }
                }
                word[i] = orig;
            }
        }
        begin_set = std::move(next_set);
        steps++;
    }
    return 0;
}
```
