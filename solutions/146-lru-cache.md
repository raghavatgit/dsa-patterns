# Problem 146: LRU Cache

## Problem Statement
Design a data structure that follows the constraints of a Least Recently Used (LRU) cache with $O(1)$ `get` and `put` operations.

## Architecture
- Hash map maps `key` to list node iterator/pointer.
- Doubly linked list maintains access recency (most recent at head, least recent at tail).

## C++ Implementation
```cpp
#include <unordered_map>

class LRUCache {
    struct Node {
        int key, value;
        Node* prev;
        Node* next;
        Node(int k, int v) : key(k), value(v), prev(nullptr), next(nullptr) {}
    };

    int capacity;
    std::unordered_map<int, Node*> cache;
    Node* head;
    Node* tail;

    void remove(Node* node) {
        node->prev->next = node->next;
        node->next->prev = node->prev;
    }

    void insertHead(Node* node) {
        node->next = head->next;
        node->prev = head;
        head->next->prev = node;
        head->next = node;
    }

public:
    LRUCache(int cap) : capacity(cap) {
        head = new Node(-1, -1);
        tail = new Node(-1, -1);
        head->next = tail;
        tail->prev = head;
    }

    int get(int key) {
        if (!cache.count(key)) return -1;
        Node* node = cache[key];
        remove(node);
        insertHead(node);
        return node->value;
    }

    void put(int key, int value) {
        if (cache.count(key)) {
            Node* node = cache[key];
            node->value = value;
            remove(node);
            insertHead(node);
            return;
        }

        if (cache.size() >= capacity) {
            Node* lru = tail->prev;
            remove(lru);
            cache.erase(lru->key);
            delete lru;
        }

        Node* new_node = new Node(key, value);
        cache[key] = new_node;
        insertHead(new_node);
    }
};
```
