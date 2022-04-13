```python
d = {}
d["George"] = 24
d["Tom"] = 32
d["Jenny"] = 16
print(d["George"])
```

    24
    


```python
print(d["Alice"])
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-2-36dc94b23fc1> in <module>
    ----> 1 print(d["Alice"])
    

    KeyError: 'Alice'



```python
d["George"] = 35
print(d["George"])
```

    35
    


```python
d[10] = 100
print(d[10])
```

    100
    


```python
print(d)
```

    {'George': 35, 'Tom': 32, 'Jenny': 16, 10: 100}
    


```python
for key, value in d.items():
    print("key:", key)
    print("value:", value)
    print(" ")
```

    key: George
    value: 35
     
    key: Tom
    value: 32
     
    key: Jenny
    value: 16
     
    key: 10
    value: 100
     
    


```python
states = {}
states["AL"] = "Alabama"
states["AK"] = "Alaska"
states["AZ"] = "Arizona"
states["AR"] = "Arkansas"
states["CA"] = "California"
states["CO"] = "Colorado"
states["CT"] = "Connecticut"
states["DE"] = "Delaware"
states["FL"] = "Florida"
states["GA"] = "Georgia"

for key, value in states.items():
    print(key + " | " + value)
```

    AL | Alabama
    AK | Alaska
    AZ | Arizona
    AR | Arkansas
    CA | California
    CO | Colorado
    CT | Connecticut
    DE | Delaware
    FL | Florida
    GA | Georgia
    

## Jonathan Doolittle


```python

```
