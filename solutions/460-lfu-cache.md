# Problem 460: LFU Cache

## Problem Statement
Design and implement a data structure for a Least Frequently Used (LFU) cache with $O(1)$ `get` and `put` time complexity.

## Complexity
- `get`: $O(1)$
- `put`: $O(1)$
- Space: $O(\text{capacity})$

## C++ Implementation
```cpp
#include <unordered_map>
#include <list>

class LFUCache {
    struct Node {
        int key, value, freq;
        Node(int k, int v) : key(k), value(v), freq(1) {}
    };

    int cap;
    int min_freq;
    std::unordered_map<int, std::list<Node>::iterator> key_map;
    std::unordered_map<int, std::list<Node>> freq_map;

    void updateFreq(std::list<Node>::iterator it) {
        int f = it->freq;
        Node node = *it;
        freq_map[f].erase(it);

        if (freq_map[f].empty()) {
            freq_map.erase(f);
            if (min_freq == f) min_freq++;
        }

        node.freq++;
        freq_map[node.freq].push_front(node);
        key_map[node.key] = freq_map[node.freq].begin();
    }

public:
    LFUCache(int capacity) : cap(capacity), min_freq(0) {}

    int get(int key) {
        if (!key_map.count(key) || cap == 0) return -1;
        auto it = key_map[key];
        int val = it->value;
        updateFreq(it);
        return val;
    }

    void put(int key, int value) {
        if (cap == 0) return;

        if (key_map.count(key)) {
            auto it = key_map[key];
            it->value = value;
            updateFreq(it);
            return;
        }

        if (key_map.size() >= cap) {
            auto victim = freq_map[min_freq].back();
            key_map.erase(victim.key);
            freq_map[min_freq].pop_back();
            if (freq_map[min_freq].empty()) freq_map.erase(min_freq);
        }

        min_freq = 1;
        freq_map[1].push_front(Node(key, value));
        key_map[key] = freq_map[1].begin();
    }
};
```
