```python
from itertools import permutations

def order(a, b, c):
    print('Unordered:')
    print(a, b, c, sep=',')
    # Swap 1
    if a > b:
        a, b = b, a
    # Swap 2
    if a > c:
        a, c = c, a
    # Swap 3
    if b > c:
        b, c = c, b
    print('Ordered:')
    print(a, b, c, sep=',')
```


```python
# For displaying all of the test cases
for combo in permutations([3, 2, 1], 3):
    order(combo[0], combo[1], combo[2])
```

    Unordered:
    3,2,1
    Ordered:
    1,2,3
    Unordered:
    3,1,2
    Ordered:
    1,2,3
    Unordered:
    2,3,1
    Ordered:
    1,2,3
    Unordered:
    2,1,3
    Ordered:
    1,2,3
    Unordered:
    1,3,2
    Ordered:
    1,2,3
    Unordered:
    1,2,3
    Ordered:
    1,2,3
    

## Jonathan Doolittle


```python

```
