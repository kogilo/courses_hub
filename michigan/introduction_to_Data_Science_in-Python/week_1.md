# Introduction to Specialization
## Why python?
* It's easy to learn
* Full featured - statistics, data acqisition, cleaning, database, more
* Strong data science libraries

# Course Outline
1. Prerequiste python knowledege
2. The pandas Toolkit
3. Advanced Querying and Manipulating with pandas
4. Basic Statistical Analysis with numpy and  scipy, and project.

# Data Science
* see `google trends` who the phrase `data science` mentioned.

# Data science
  1. Data Exploration and preparation
  2. Data Representation and Transformation
  3. Computing with data
  4. Date Modeling
  5. Data Visualization and Representation
  6. Science about Data Science
# The Coursera Jupyter Notebook System

# Python Functions
  * Python is a `high level language`, which means it's `optimized for reading by people instead of machines`.
  It's also an `interpreted language` which means it isn't `compiled directly` to machine code and importantly is commonly used in an interactive fashion.
  * Example
  ```python
  x = 1
  y=2
  x+y
  x
  ```
  * doesn't require key word like  `var` to declare the variable.
```python
  def add_numbers(x,y,z):
      return x+y+z
  print(add_numbers(1,2,3))
```
* add_numbers updated to take an optional 3rd parameter. Using print allows printing of multiple expressions within a single cell.
```python
def add_numbers(x,y,z=None):
    if (z==None):
        return x+y
    else:
        return x+y+z

print(add_numbers(1, 2))
print(add_numbers(1, 2, 3))
```
* add_numbers updated to take an optional flag parameter.
```python
def add_numbers(x, y, z=None, flag=False):
    if (flag):
        print('Flag is true!')
    if (z==None):
        return x + y
    else:
        return x + y + z

print(add_numbers(1, 2, flag=True))
```
* Assign function add_numbers to variable a.
```python
def add_numbers(x,y):
    return x+y

a = add_numbers
a(1,2)
```

# The Python Programming Language: Types and Sequences
* Use `type()` function to return the object's `type`.
```python
type("This is a string")
```
```python
type(None)
```

```python
type(1)
```

```python
type(1.0)
```
```python
type(add_numbers)
```
* `Tuples` are an immutable data structure (cannot be altered).

```python
x = (1, 'a', 2, 'b')
type(x)
```
* `Lists` are a mutable data structure.
```python
x = [1, 'a', 2, 'b']
type(x)
```

* Use append to append an object to a list.
```python
x.append(3.3)
print(x)
```

* This is an example of how to loop through each item in the list.
```python
for item in x:
    print(item)
```
* Or using the indexing operator:
```python
i=0
while( i != len(x) ):
    print(x[i])
    i = i + 1
```

* Use + to concatenate lists.
```python
[1,2] + [3,4]
```
* Use * to repeat lists.

```python
[1]*3
```
* Use the in operator to check if something is inside a list.

```python
1 in [1, 2, 3]
```
* Now let's look at strings. Use bracket notation to slice a string.
```python
x = 'This is a string'
print(x[0]) #first character
print(x[0:1]) #first character, but we have explicitly set the end character
print(x[0:2]) #first two characters
```
* This will return the last element of the string.
```python
x[-1]
```
* This will return the slice starting from the 4th element from the end and stopping before the 2nd element from the end.
```python
x[-4:-2]
```
* This is a slice from the beginning of the string and stopping before the 3rd element.
```python
x[:3]
```
* And this is a slice starting from the 4th element of the string and going all the way to the end.
```python
x[3:]
```

```python
firstname = 'Christopher'
lastname = 'Brooks'
print(firstname + ' ' + lastname)
print(firstname*3)
print('Chris' in firstname)
```
* `split` returns a list of all the words in a string, or a list split on a specific character.

```python
firstname = 'Christopher Arthur Hansen Brooks'.split(' ')[0] # [0] selects the first element of the list
lastname = 'Christopher Arthur Hansen Brooks'.split(' ')[-1] # [-1] selects the last element of the list
print(firstname)
print(lastname)
```
* Make sure you convert objects to strings before concatenating.
```python
'Chris' + 2
```
```python
'Chris' + str(2)
```

* Dictionaries associate keys with values.
