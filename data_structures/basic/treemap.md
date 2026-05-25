# TreeMap

A TreeMap stores key-value pairs in sorted key order, typically backed by a Red-Black tree or AVL tree. Python has no built-in TreeMap; the `sortedcontainers` package provides `SortedDict`.

## Complexity

| Operation | Time |
|---|---|
| Lookup / Insert / Delete | O(log n) |
| Iteration (sorted order) | O(n) |

## Python Usage

```python
# pip install sortedcontainers
from sortedcontainers import SortedDict

tm = SortedDict()
tm['c'] = 3; tm['a'] = 1; tm['b'] = 2
for key in tm:              # a, b, c in order
    print(key, tm[key])
print('b' in tm)            # True
del tm['a']
```
