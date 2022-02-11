# Loops and Conditionals

## For Loops

A for loop is used for iterating over a sequence. The sequence can be a list, a tuple, a dictionary, a set, or a string.




```python
cities = ['San Francisco', 'Los Angeles', 'New York', 'Atlanta']

for city in cities:
    print(city)
```

To iterate over a dictionary, you can call the `items()` method on it which returns a tuple of key and value for each item.


```python
data = {'city': 'San Francisco', 'population': 881549, 'coordinates': (-122.4194, 37.7749) }

for x, y in data.items():
    print(x, y)
```

The built-in `range()` function allows you to create sequence of numbers that you can iterate over


```python
for x in range(5):
    print(x)
```

The range function can also take a start and an end number


```python
for x in range(1, 10, 2):
    print(x)
```

# Conditionals

Python supports logical conditions such as equals, not equals, greater than etc. These conditions can be used in several ways, most commonly in *if statements* and loops.

An *if statement* is written by using the `if` keyword.

Note: A very common error that programmers make is to use *=* to evaluate a *equals to* condition. The *=* in Python means assignment, not equals to. Always ensure that you use the *==* for an equals to condition.


```python
for city in cities:
    if city == 'Atlanta':
        print(city)
```

You can use `else` keywords along with `if` to match elements that do not meet the condition


```python
for city in cities:
    if city == 'Atlanta':
        print(city)
    else:
        print('This is not Atlanta')
```

Python relies on indentation (whitespace at the beginning of a line) to define scope in the for loop and if statements. So make sure your code is properly indented. 

You can evaluate a series of conditions using the `elif` keyword.

Multiple criteria can be combined using the `and` and `or` keywords.


```python
cities_population = {
    'San Francisco': 881549,
    'Los Angeles': 3792621,
    'New York': 8175133,
    'Atlanta':498044
}

for city, population in cities_population.items():
    if population < 1000000:
        print('{} is a small city'.format(city))
    elif population > 1000000 and population < 5000000:
        print('{} is a big city'.format(city))
    else:
        print('{} is a mega city'.format(city))
```

## Control Statements

A for-loop iterates over each item in the sequence. Sometimes is desirable to stop the execution, or skip certain parts of the for-loops. Python has special statements, `break`, `continue` and `pass`. 

A `break` statement will stop the loop and exit out of it


```python
for city in cities:
    print(city)
    if city == 'Los Angeles':
        print('I found Los Angeles')
        break
```

A `continue` statement will skip the remaining part of the loop and go to the next iteration


```python
for city in cities:
    if city == 'Los Angeles':
        continue
    print(city)
```

A `pass` statement doesn't do anything. It is useful when some code is required to complete the syntax, but you do not want any code to execute. It is typically used as a placeholder when a function is not complete.


```python
for city in cities:
    if city == 'Los Angeles':
        pass
    else:
        print(city)
```

## Exercise

The Fizz Buzz challenge.

Write a program that prints the numbers from 1 to 100 and for multiples of 3 print **Fizz** instead of the number and for the multiples of 5 print **Buzz**. If it is divisible by both, print **FizzBuzz**.

So the output should be something like below

`1, 2, Fizz, 4, Buzz, Fizz, 7, 8, Fizz, Buzz, 11, Fizz, 13, 14, FizzBuzz, ...`

Breaking down the problem further, we need to create for-loop with following conditions

- If the number is a multiple of both 3 and 5 (i.e. 15), print FizzBuzz
- If the number is multiple of 3, print Fizz
- If the number is multiple of 5, print Buzz
- Otherwise print the number

Hint: See the code cell below. Use the modulus operator **%** to check if a number is divisible by another. `10 % 5` equals 0, meaning it is divisible by 5.



```python
for x in range(1, 10):
    if x%2 == 0:
        print('{} is divisible by 2'.format(x))
    else:
        print('{} is not divisible by 2'.format(x))
```

----
