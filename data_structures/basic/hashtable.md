# Hashtable

A hashtable (hash map, dictionary, or hash set) maps keys to values using a hash function for O(1) average lookups.

## Complexity

| Operation | Average |
|---|---|
| Lookup / Insert / Delete | O(1) |
| Iteration | O(n) |

## Collision Handling

- **Chaining**: Store colliding entries in a linked list at the same index.
- **Open Addressing**: Probe for the next available slot.

## Python Usage

### dict (hash map)

```python
d = {"apple": 5, "banana": 3}
d["orange"] = 8
print(d["apple"], d.get("pear", 0))
del d["banana"]
"orange" in d            # membership
for k, v in d.items():   # iterate
d.clear()
```

### set (hash set)

```python
s = set()
s.add(10); s.add(20)
10 in s                   # True
s.remove(10)              # raises KeyError if missing
s.discard(50)             # safe remove
len(s); s.clear()
```

## Related LeetCode Questions

- [1. Two Sum](../../leetcode_questions/1_two_sum.md)
- [217. Contains Duplicate](../../leetcode_questions/217_contain_duplicate.md)
