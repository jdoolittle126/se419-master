```python
# This is a comment line

# This is a comment Line 
# Use hashtag or pound symbol to start a comment 
# Functions is a collection of instructions (code) 
def function1(): 
    print("hi") 
    print("hi 2") 
print("this is outside the function") 
```

    this is outside the function
    


```python
function1()
```

    hi
    hi 2
    


```python
# a mapping
def function2(x):
    return 2 * x
```


```python
a = function2(3)
print(a)
```

    6
    


```python
d = function2()
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-6-9f9e7aec7a86> in <module>
    ----> 1 d = function2()
    

    TypeError: function2() missing 1 required positional argument: 'x'



```python
def function3(x, y):
    return x + y
```


```python
e = function3(1, 2)
print(e)
```

    3
    


```python
def function4(some_argument):
    print(some_argument)
    print("weee")
```


```python
function4("hello")
function4(55)
```

    hello
    weee
    55
    weee
    


```python
# BMI calculator function
name1 = "Jean"
height_m1 = 2
weight_kg1 = 90

name2 = "Jean's sister"
height_m2 = 1.8
weight_kg2 = 70

name3 = "Jean's brother"
height_m3 = 2.5
weight_kg3 = 160
```


```python
def bmi_calculator(name, height_m, weight_kg):
    bmi = weight_kg / (height_m ** 2)
    print("bmi: ")
    print(bmi)
    if bmi < 25:
        return name + " not overweight"
    else:
        return name + " is overweight"
```


```python
result1 = bmi_calculator(name1, height_m1, weight_kg1)
print(result1)
```

    bmi: 
    22.5
    Jean not overweight
    


```python
result2 = bmi_calculator(name2, height_m2, weight_kg2)
print(result2)

result3 = bmi_calculator(name3, height_m3, weight_kg3)
print(result3)
```

    bmi: 
    21.604938271604937
    Jean's sister not overweight
    bmi: 
    25.6
    Jean's brother is overweight
    


```python
def convert(miles):
    return 1.6 * miles

print("5 miles in km is " + str(convert(5)) + "km")
```

    5 miles in km is 8.0km
    

## Jonathan Doolittle


```python

```
