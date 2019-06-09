
# Fibonacci Sequence

The *Fibonacci Sequence* is the series of numbers:

**0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...**

The next number is found by adding up the two numbers before it.

* The 2 is found by adding the two numbers before it (1+1)
* The 3 is found by adding the two numbers before it (1+2),
* And the 5 is (2+3),
* and so on!

The rule of *Fibonacci Sequence* is 

*$x_n = x_{n-1} + x_{n-2}$*

where:

$x_n$ is term number "n"   
$x_{n-1}$ is the previous term (n-1)   
$x_{n-2}$ is the term before that (n-2)   

*source* : https://www.mathsisfun.com/numbers/fibonacci-sequence.html



### Let's implement this rule with Python


```python
import time
```


```python
def test_fibonacci(function_name, counts=40):
    result = {}
    for i in range(0, counts + 1):
         print(f'{i} : {function_name(i):,}')                       
```

## With for loop


```python
# using for loop 

def fibonacci_loop(num):
    if num == 0:
        return 0
    elif num == 1 or num == 2:
        return 1
    elif num > 2:
        a = 1 # variable for (n - 1)
        b = 1 # variable for (n - 2)
        for _ in range(3, num + 1):
            c = a + b
            a, b = b, c
            
        return c
```


```python
test_fibonacci(fibonacci_loop)
```

    0 : 0
    1 : 1
    2 : 1
    3 : 2
    4 : 3
    5 : 5
    6 : 8
    7 : 13
    8 : 21
    9 : 34
    10 : 55
    11 : 89
    12 : 144
    13 : 233
    14 : 377
    15 : 610
    16 : 987
    17 : 1,597
    18 : 2,584
    19 : 4,181
    20 : 6,765
    21 : 10,946
    22 : 17,711
    23 : 28,657
    24 : 46,368
    25 : 75,025
    26 : 121,393
    27 : 196,418
    28 : 317,811
    29 : 514,229
    30 : 832,040
    31 : 1,346,269
    32 : 2,178,309
    33 : 3,524,578
    34 : 5,702,887
    35 : 9,227,465
    36 : 14,930,352
    37 : 24,157,817
    38 : 39,088,169
    39 : 63,245,986
    40 : 102,334,155



```python
%time fibonacci_loop(40)
```

    CPU times: user 6 µs, sys: 0 ns, total: 6 µs
    Wall time: 8.11 µs





    102334155



## With recursion

We can solve the problem with for-loop, but it is not so intuitive. <br>
From the rule of fibonacci sequence *($x_n = x_{n-1} + x_{n-2}$)*  , <br> 
we can make a function that call itself,
it is called *recursive* function.


```python
# Recursive Method 1 : traditional recursive function

def fibonacci_recursion(num):
    '''Return a fibonacci sequence value of num'''
    if num == 0:
        return 0
    if num == 1 or num == 2:
        return 1
    
    return fibonacci_recursion(num - 2) + fibonacci_recursion(num - 1)

```


```python
# Test with recursion
test_fibonacci(fibonacci_recursion)
```

    0 : 0
    1 : 1
    2 : 1
    3 : 2
    4 : 3
    5 : 5
    6 : 8
    7 : 13
    8 : 21
    9 : 34
    10 : 55
    11 : 89
    12 : 144
    13 : 233
    14 : 377
    15 : 610
    16 : 987
    17 : 1,597
    18 : 2,584
    19 : 4,181
    20 : 6,765
    21 : 10,946
    22 : 17,711
    23 : 28,657
    24 : 46,368
    25 : 75,025
    26 : 121,393
    27 : 196,418
    28 : 317,811
    29 : 514,229
    30 : 832,040
    31 : 1,346,269
    32 : 2,178,309
    33 : 3,524,578
    34 : 5,702,887
    35 : 9,227,465
    36 : 14,930,352
    37 : 24,157,817
    38 : 39,088,169
    39 : 63,245,986
    40 : 102,334,155



```python
%time fibonacci_recursion(40)
```

    CPU times: user 26.5 s, sys: 64 ms, total: 26.6 s
    Wall time: 26.6 s





    102334155



## Quiet slow??

It takes more and more time while the number is increased.  
Because the function itself is needed to calculate same value over and over.    
We can reduce total number of calling the function with saving the result to **cache**.


```python
# Recursive Method 2 : With using explicit cache
cache = {}

def fibonacci_cache(num):
    '''Return a fibonacci sequence value of num'''

    if num in cache:
        return cache[num]

    if num == 0:
        result = 0
    elif num == 1 or num == 2:
        result = 1
    else:
        result = fibonacci_cache(num - 2) + fibonacci_cache(num - 1)
    
    cache[num] = result
    return result

```


```python
# Test with using explicit cache
test_fibonacci(fibonacci_cache)
```

    0 : 0
    1 : 1
    2 : 1
    3 : 2
    4 : 3
    5 : 5
    6 : 8
    7 : 13
    8 : 21
    9 : 34
    10 : 55
    11 : 89
    12 : 144
    13 : 233
    14 : 377
    15 : 610
    16 : 987
    17 : 1,597
    18 : 2,584
    19 : 4,181
    20 : 6,765
    21 : 10,946
    22 : 17,711
    23 : 28,657
    24 : 46,368
    25 : 75,025
    26 : 121,393
    27 : 196,418
    28 : 317,811
    29 : 514,229
    30 : 832,040
    31 : 1,346,269
    32 : 2,178,309
    33 : 3,524,578
    34 : 5,702,887
    35 : 9,227,465
    36 : 14,930,352
    37 : 24,157,817
    38 : 39,088,169
    39 : 63,245,986
    40 : 102,334,155



```python
%time fibonacci_cache(40)
```

    CPU times: user 2 µs, sys: 0 ns, total: 2 µs
    Wall time: 5.01 µs





    102334155



 same result but super faster than normal recursive function

## Using LRU cache

Python provides a **functools** library  helps the recursive function calls,   
let's use Least Recently Used cache *(lru_cache)* from functools


```python
# import library
from functools import lru_cache
```


```python
# Recursive Method 3 : with implicit cache provided by functools

# set cache with 1000 (need to set a big values, small cache is NOT useful)
@lru_cache(maxsize = 1000)

def fibonacci(num):
    '''Return a fibonacci sequence value of num'''

    if num == 0:
        return 0
    if num == 1 or num == 2:
        return 1
    
    return fibonacci(num - 2) + fibonacci(num - 1)
```


```python
test_fibonacci(fibonacci)
```

    0 : 0
    1 : 1
    2 : 1
    3 : 2
    4 : 3
    5 : 5
    6 : 8
    7 : 13
    8 : 21
    9 : 34
    10 : 55
    11 : 89
    12 : 144
    13 : 233
    14 : 377
    15 : 610
    16 : 987
    17 : 1,597
    18 : 2,584
    19 : 4,181
    20 : 6,765
    21 : 10,946
    22 : 17,711
    23 : 28,657
    24 : 46,368
    25 : 75,025
    26 : 121,393
    27 : 196,418
    28 : 317,811
    29 : 514,229
    30 : 832,040
    31 : 1,346,269
    32 : 2,178,309
    33 : 3,524,578
    34 : 5,702,887
    35 : 9,227,465
    36 : 14,930,352
    37 : 24,157,817
    38 : 39,088,169
    39 : 63,245,986
    40 : 102,334,155



```python
%time fibonacci(40)
```

    CPU times: user 3 µs, sys: 0 ns, total: 3 µs
    Wall time: 5.25 µs





    102334155



Little differ time values, but it could be ignored. (just some micro seconds)

## Conclusion

**We need to set *lru_cache* when using recursive function for performance**


```python

```
