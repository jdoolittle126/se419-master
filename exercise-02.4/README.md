```python
a = [3, 10, -1]
```


```python
print(a)
```

    [3, 10, -1]
    


```python
a.append(1)
print(a)
```

    [3, 10, -1, 1]
    


```python
a.append("hello")
print(a)
```

    [3, 10, -1, 1, 'hello']
    


```python
a.append([1, 2])
print(a)
```

    [3, 10, -1, 1, 'hello', [1, 2]]
    


```python
a.pop()
```




    [1, 2]




```python
print(a)
```

    [3, 10, -1, 1, 'hello']
    


```python
a[0]
```




    3




```python
a[0] = 100
print(a)
```

    [100, 10, -1, 1, 'hello']
    


```python
b = ["banana", "apple", "microsoft"]
temp = b[0]
b[0] = b[1]
b[1] = temp
print(b)
```

    ['apple', 'banana', 'microsoft']
    


```python
b[0], b[1] = b[1], b[0]
print(b)
```

    ['banana', 'apple', 'microsoft']
    


```python
print(a[-1])
```

    hello
    


```python
a[1:3]
```




    [10, -1]




```python
a[:3]
```




    [100, 10, -1]




```python
a[2:]
```




    [-1, 1, 'hello']




```python
a[0:2] = ["lisa", 1.74]
a
```




    ['lisa', 1.74, -1, 1, 'hello']




```python
a + ["me", 1.79]
```




    ['lisa', 1.74, -1, 1, 'hello', 'me', 1.79]




```python
del(a[0])
```


```python
a
```




    [1.74, -1, 1, 'hello']




```python
x = ["a", "b", "c"]
y = list(x)
y
```




    ['a', 'b', 'c']



## Jonathan Doolittle


```python

```
