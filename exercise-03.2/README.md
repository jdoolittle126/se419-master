```python
a = "hello there"
a.find("there")
```




    6




```python
a.find("HELLO")
```




    -1




```python
file = open("yesno.txt", "r")
```


```python
lines = file.readlines()
```


```python
file.close()
```


```python
print(lines)
```

    ['YES\n', 'NO\n', 'YES\n', 'YES\n', 'YES\n', 'NO\n', 'YES\n', 'YES']
    


```python
countYes = 0
countNo = 0
```


```python
for line in lines:
    line = line.strip().upper()
    
    if line.find("YES") != -1 and len(line) == 3:
        countYes = countYes + 1
    if line.find("NO") != -1 and len(line) == 2:
        countNo = countNo + 1
```


```python
print("Yes: ", countYes)
print("No: ", countNo)
```

    Yes:  6
    No:  2
    

## Jonathan Doolittle


```python

```
