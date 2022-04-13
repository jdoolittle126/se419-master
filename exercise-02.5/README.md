```python
a = ["banana", "apple", "microsoft"]
print(a[0])
print(a[1])
print(a[2])
```

    banana
    apple
    microsoft
    


```python
for element in a:
    print(element)
```

    banana
    apple
    microsoft
    


```python
for element in a:
    print(element)
    print(element)
```

    banana
    banana
    apple
    apple
    microsoft
    microsoft
    


```python
b = [20, 10, 5]
for e in b:
    print(e)
```

    20
    10
    5
    


```python
b = [20, 10, 5]
total = 0
for e in b:
    total = total + e
print(total)
```

    35
    


```python
range(1, 5)
```




    range(1, 5)




```python
total = 0
for e in range(1, 100):
    total = total + e
print(total)
```

    4950
    


```python
c = list(range(1, 5))
```


```python
print(c)
```

    [1, 2, 3, 4]
    


```python
for i in range(1, 5):
    print(i)
```

    1
    2
    3
    4
    


```python
print(list(range(1, 8)))
```

    [1, 2, 3, 4, 5, 6, 7]
    


```python
total3 = 0
for i in range(1, 8):
    if i % 3 == 0:
        total3 += i
        
print(total3)
```

    9
    


```python
total35 = 0
for i in range(1, 100):
    if i % 3 == 0 and i % 5 == 0:
        total35 += i
        
print(total35)
```

    315
    

## Jonathan Doolittle


```python

```
