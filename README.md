# Python: Quick & dirty

## Introduction
Python is a programming* language made to do quick and dirty things. The syntax is simple and clear, easy to read and accesible, BUT it's _terribly_ inefficient.  
It's a the perfect language for prototyping or doing simple stuff, but if you want any kind of performance or are working on complex things, I'd suggest something like C++, C#, Java, or Rust.  


## General characteristics
- Object-oriented
- Garbage-collected (you don't have to manage memory)
- Interpreted.  This means you need to have an interpreter to run any Python script, but also that you can program through a Python terminal/interpreter (useful for testing stuff).  
Python is more of an scripted language, you create scripts where each instruction is run sequentially. If something on your script is below the current line, _it doesn't exist_.  
- It lets you do a lot of stupid stuff and _spaghetti code_, so be careful.

To run a script, run the interpreter and specify the script name:
```bash
python3 script.py
```


## General syntax
- Every instruction ends with an _endline_ (carriage return), no `;` or any bullshit.
- Code blocks are delimeted by indentation, so it's compulsory to _correctly_ indent your code.  
Use tabs or 4 spaces, but **do not mix**.
- Double quotes (`"`) and single quotes (`'`) have the same use, but **don't mix them**.
- You comment with `#`, and block comments are made with quotes.
```python
# this is a line comment

"""
This is a 
block comment
"""
```


## Variables
- Can hold any type (reusable), and you don't have to declare it.
- Need to declare and initialize a variable on the same line.
- No variable is constant
```python
foo = 0
foo = "stuff"
```
- The scope (where you can access the variable) is local, that means, the function it is contained in.
- All other variables are global.
- To create or modify a global variable inside a function, use the keyword `global`.
```python
a = 0              # global variable

def func():
    b = a + 1      # local variable, using global a
    global c       # create global c
    c = 2         
    global a       # access global a
    a = "xd"       # modify a

func()

c += 4             # update c
b -= 1             # this won't work, b is out of scope
```


## Data types
- `int`: Integers without limit (memory limited).
- `float`: Floating point, single/double precision.
- `complex`: Complex numbers, real + imaginary part (j).  
Can use integer or floating point numbers.
- `bool`: Booleans. `True`/`False`.
- `str`: Variable length strings (ASCII characters).
- `None`: No value.

```python
a = 69          # int
b = 4.20        # float
c = 4 + 20.69j  # complex
d = False       # bool
e = "caca"      # str
```

### Castings
Datatypes are converted automatically, but you can force them by using functions like `int()`, `float()`, `str()`, `bool()`, etc.  
They have different behaviours depending on the types.

```python
>>> a = 69
>>> b = str(a)  # casting int → str
>>> b
'69'
```


## Input/Output
- `print()` outputs strings or variables (converted to strings).  
You can concatenate them using commas (adds a space in between).
- `input()` returns a keyboard input as a string.

```python
name = input()
print("Hello", name, "\b!")
print("\nHow are you?")
```

Example output:
```
Hello Pepe!

How are you?
```

## Data structures

### List (linked list) - `[elem1, elem2, <...>]`

- Heterogeneous (allows different types)
- Can be expanded and modified
- Can be nested: `[[elem00, elem01], elem1]`. Useful for matrices.
```python
>>> matrix = ([0,1],[2,3])
>>> matrix[1][0]
2
```
- Assigning one list to a new variable doesn't copy the list, just the head pointer, so changes to the old list affect the new one.  
Use `newList = oldList.copy()`.
```python
>>> a = [0, 1]
>>> b = a
>>> a[0] = 1
>>> b
[1, 1]
```
- You can unpack a list to several variables:
```python
>>> myList = [0, True, "xd"]
>>> a, b, c = myList
>>> print(a,b,c)
0 True xd
```

Some methods:
- `var.append(elem)`: Adds _elem_ to the end of the list _var_.
- `var.pop(pos)`: Removes and return the element at position _pos_ of the list _var_.
- `var.insert(pos, elem)`: Adds _elem_ to the list _var_ at _pos_.


<!-- ### Dictionaries -->


## Operators
- Assign: `=`
- Arithmetic: `+`, `-`, `*`, `/` (can also be applied to strings and lists)
- Divisors: `%` (remainder) and `//` (integer division)

All those can be combined with the assign operator: `+=`, `-=`, etc.  
When in doubt of the order of precedence of operators, use parenthesis.

The following are used to evaluate expressions, and return an boolean:
- Relational: `==`, `<`, `>`, `>=`, `<=`, `!=`
- Logical: `and`, `or`, `not`
- Membership: `in`, `not in`. To see if something is inside another thing.

```python
>>>"end" in "friend"
True
```

- Positional: In strings and lists, you can access specific elements or sub-elements
    - `var[n]` accesses the element of index _n_
    - `var[-n]` accesses the element of index _n_, but starting from the back (the last one is accessed with `var[-1]`)
    - `var[n:]` accesses the sub-elements between index _n_ and the end.
    - `var[:n]` accesses the sub-elements between the beginning and index _n_.
    - `var[n:m]` accesses the sub-elements between index _n_ and _m-1_.

```bash
>>> a = "@guluc3m"
>>> a[8]
IndexError: string index out of range
>>> a[0]
'@'
>>> a[-1]
'm'
>>> a[1:4]
'gul'
>>> a[4:]
'uc3m'
```


## Control flow
- If - `if condition:`.  
_condition_ must be a boolean
- Else - `else:`.  
- Elif - `elif condition:`.
```python
if a == 69:
    b = "nice"
elif a in sumStuff:
    b = True
else:
    b = False
```
Remember that indentation matters.


## Loops
- While - `while condition:`  
_condition_ is checked at the beginning of the iteration.
- For (for each) - `for elem in object:`  
Traverses the elements of _object_, assinging the element to _elem_ each iteration, and exits the loop once it reaches the end of _object_.  
You can implement a regular for loop using `for i in range(max)`.

```python
>>> a = (1, True, "a")
>>> b = []
>>> i = 0
>>> for elem in a:
...     b[i] = elem
...     i += 1
>>> b
[1, True, "a"]
```

- You can use `break` to exit a loop at any point and `continue` to stop the current iteration and start the next one.


## Functions
`def function(param1, ...):`
- Can return any type, or nothing.
- Uses pass by value for datatypes and pass by reference for structures and objects.
- You can define default values for parameters: `def function(param = 0)`.
- Can return multiple values: `return var1, var2`.  
Remember to unload them after calling the function.

```python
def divide(a, b = 1):
	c = a//b
	r = a%b
	return c, r

coc, res = divide(3)
```


## Read/Write files
Use the `open()` function.

### Reading
- You can read the whole file with the `read()` method, returning a string with breaklines.
```python
with open("file") as f:
    text = f.read()
```

- You can also read files line by line, using a for loop.
```python
with open("file") as f:
    text = []
    for line in f:
        pass   # do whatever
```

### Writting

I recommend to always append to the end of the file (`"a"` parameter)
```python
with open("file", "a") as f:
    f.write(text)
```
Remember to add `"\n"` at the end for a new line.


<!-- ## `pip` and modules -->


## Extra stuff
- This is a summarized version of a talk I gave (**in spanish**) for the [GUL](https://gul.uc3m.es) university association, you can find the video [here](https://www.youtube.com/watch?v=1xA0d7Z4EgU&t=1398s) and the slides [here](https://docs.google.com/presentation/d/1EItWmCZvpOq0B9ViRJrJD5C6bgc5sKP2h5glHTSwxog/edit?usp=sharing).
- Python tutorials can be found in [W3Schools](w3schools.com/python/).
