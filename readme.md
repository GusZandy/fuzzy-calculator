# **FUZZY CALCULATOR PROGRAM**

# 1. Fuzzy Set Operators

## - Transpose


```python
def trans(x: list):
    data = []
    for i in range(len(x[0])):
        temp = []
        for j in range(len(x)):
            temp.append(x[j][i])
        data.append(temp)
    return data
```

## - S-Norm


```python
def s_norm(x, y):
    if isinstance(x, list) and isinstance(y, list):
        if isinstance(x[0], list) and isinstance(y[0], list):
            return [[x[i][j]+y[i][j]-x[i][j]*y[i][j] for j in range(len(x[0]))] for i in range(len(x))]
        else: 
            return [x[i]+y[i]-x[i]*y[i] for i in range(len(x))] 
    else:
        return x+y-x*y # algebraic sum
```

## - T-Norm


```python
def t_norm(x: list, y: list):
    if isinstance(x, list) and isinstance(y, list):
        if isinstance(x[0], list) and isinstance(y[0], list):
            return [[x[i][j]*y[i][j] for j in range(len(x[0]))] for i in range(len(x))]
        else: 
            return [x[i]*y[i] for i in range(len(x))]
    else:
        return x*y
```

## - C-Std


```python
def c_std(x: list):
    if isinstance(x, list):
        if isinstance(x[0], list):
            return [[1-x[i][j] for j in range(len(x[0]))] for i in range(len(x))]
        else: 
            return [1-x[i] for i in range(len(x))]
    else:
        return 1-x
```

# 2. Fuzzy Relation

## - S-Norm Relation


```python
def s_norm_relation(x: list, y: list):
    data = []
    for i in range(len(x)):
        temp = []
        for j in range(len(y)):
            temp.append(s_norm(x[i], y[j]))
        data.append(temp)
    return data
```

## - T-Norm Relation


```python
def t_norm_relation(x: list, y: list):
    data = []
    for i in range(len(x)):
        temp = []
        for j in range(len(y)):
            temp.append(t_norm(x[i], y[j]))
        data.append(temp)
    return data
```

## - Composition


```python
def composition(x: list, y:list):
    if len(x) == len(y[0]) and len(y) == len(x[0]):
        data = []
        for i in range(len(x)):
            temp = []
            for j in range(len(x)):
                a = x[i]
                b = [y[t][j] for t in range(len(y))]
                temp.append(max([a[t]*b[t] for t in range(len(y))]))
            data.append(temp)
        return data
    else:
        return 0
```

# 3.Linguistic Operators

## - Hedges


```python
def rather(u):
    if isinstance(u, list):
        if isinstance(u[0], list):
            return [[u[i][j]**0.5 for j in range(len(u[0]))] for i in range(len(u))]
        else:
            return [u[i]**0.5 for i in range(len(u))]
    else:        
        return u**0.5

def very(u):
    if isinstance(u, list):
        if isinstance(u[0], list):
            return [[u[i][j]**2 for j in range(len(u[0]))] for i in range(len(u))]
        else:
            return [u[i]**2 for i in range(len(u))]
    else:        
        return u**2
```

# Examples

## - Fuzzy Set Operators

### C-Std, S-Norm, and T-Norm


```python
A = [ 0, 0.1, 0.3, 0.5, 0.6, 0.8]
B = [ 0.8, 1, 0.9, 0.7, 0.5, 0.3]
```


```python
c_std(A)
```




    [1, 0.9, 0.7, 0.5, 0.4, 0.19999999999999996]




```python
c_std(B)
```




    [0.19999999999999996, 0, 0.09999999999999998, 0.30000000000000004, 0.5, 0.7]




```python
s_norm(A,B)
```




    [0.8, 1.0, 0.9299999999999999, 0.85, 0.8, 0.8600000000000001]




```python
t_norm(A,B)
```




    [0.0, 0.1, 0.27, 0.35, 0.3, 0.24]



## - Fuzzy Relation


```python
A = [0, 0.3, 0.5, 0.7, 0.9, 1]
B = [0.8, 0.5, 0.1, 0.3]
C = [[1.00, 0.80, 0.60, 0.40, 0.20, 0.00],
     [0.8, 1, 0.8, 0.6, 0.4, 0.2],
     [0.6, 0.8, 1, 0.8, 0.6, 0.4],
     [0.4, 0.6, 0.8, 1, 0.8, 0,6]]
R = [[i+j-i*j for j in B] for i in A]
```


```python
R
```




    [[0.8, 0.5, 0.1, 0.3],
     [0.8600000000000001, 0.65, 0.37, 0.51],
     [0.9, 0.75, 0.5499999999999999, 0.65],
     [0.9400000000000001, 0.85, 0.73, 0.79],
     [0.9800000000000001, 0.95, 0.91, 0.9299999999999999],
     [1.0, 1.0, 1.0, 1.0]]



### 1. CoR (C composition R)


```python
composition(C,R)
```




    [[0.8, 0.52, 0.32999999999999996, 0.40800000000000003],
     [0.8600000000000001, 0.65, 0.43999999999999995, 0.52],
     [0.9, 0.75, 0.584, 0.65],
     [0.9400000000000001, 0.85, 0.73, 0.79]]



### 2. RoC (R composition C)


```python
composition(R,C)
```




    [[0.8, 0.6400000000000001, 0.48, 0.32000000000000006, 0.24, 0.1],
     [0.8600000000000001,
      0.6880000000000002,
      0.52,
      0.51,
      0.40800000000000003,
      0.148],
     [0.9, 0.75, 0.6000000000000001, 0.65, 0.52, 0.21999999999999997],
     [0.9400000000000001, 0.85, 0.73, 0.79, 0.6320000000000001, 0.292],
     [0.9800000000000001,
      0.95,
      0.91,
      0.9299999999999999,
      0.744,
      0.36400000000000005],
     [1.0, 1.0, 1.0, 1.0, 0.8, 0.4]]



## 3. R transpose


```python
R_trans = trans(R)
R_trans
```




    [[0.8, 0.8600000000000001, 0.9, 0.9400000000000001, 0.9800000000000001, 1.0],
     [0.5, 0.65, 0.75, 0.85, 0.95, 1.0],
     [0.1, 0.37, 0.5499999999999999, 0.73, 0.91, 1.0],
     [0.3, 0.51, 0.65, 0.79, 0.9299999999999999, 1.0]]



### 2. RoR_transpose (R composition R_transpose)


```python
composition(R, R_trans)
```




    [[0.6400000000000001,
      0.6880000000000002,
      0.7200000000000001,
      0.7520000000000001,
      0.7840000000000001,
      0.8],
     [0.6880000000000002,
      0.7396000000000001,
      0.7740000000000001,
      0.8084000000000001,
      0.8428000000000002,
      0.8600000000000001],
     [0.7200000000000001,
      0.7740000000000001,
      0.81,
      0.8460000000000001,
      0.8820000000000001,
      0.9],
     [0.7520000000000001,
      0.8084000000000001,
      0.8460000000000001,
      0.8836000000000002,
      0.9212000000000001,
      0.9400000000000001],
     [0.7840000000000001,
      0.8428000000000002,
      0.8820000000000001,
      0.9212000000000001,
      0.9604000000000001,
      0.9800000000000001],
     [0.8, 0.8600000000000001, 0.9, 0.9400000000000001, 0.9800000000000001, 1.0]]



## - Linguistic Operators


```python
A = [ 0, 0.1, 0.3, 0.5, 0.6, 0.8]
B = [ 0.8, 1, 0.9, 0.7, 0.5, 0.3]
```

### 1. Not A


```python
not_A = c_std(A)
not_A
```




    [1, 0.9, 0.7, 0.5, 0.4, 0.19999999999999996]



### 2. Very A


```python
very_A = very(A)
very_A
```




    [0, 0.010000000000000002, 0.09, 0.25, 0.36, 0.6400000000000001]



### 3. Rather A


```python
rather_A = rather(A)
rather_A
```




    [0.0,
     0.31622776601683794,
     0.5477225575051661,
     0.7071067811865476,
     0.7745966692414834,
     0.8944271909999159]



### 4. Not A AND B


```python
t_norm(not_A, B)
```




    [0.8, 0.9, 0.63, 0.35, 0.2, 0.059999999999999984]



### 5. Very Not A


```python
very(not_A)
```




    [1, 0.81, 0.48999999999999994, 0.25, 0.16000000000000003, 0.03999999999999998]



### 6. Not B


```python
not_B = c_std(B) 
not_B
```




    [0.19999999999999996, 0, 0.09999999999999998, 0.30000000000000004, 0.5, 0.7]



### 7. Rather Not B


```python
rather(not_B)
```




    [0.44721359549995787,
     0.0,
     0.3162277660168379,
     0.5477225575051662,
     0.7071067811865476,
     0.8366600265340756]


