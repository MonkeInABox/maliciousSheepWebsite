---
title: CITS2401 Notes
description: Uni Notes
layout: default.hbs
---

<a class="link" href="./notes.html">cd -</a>

>Written by Jeremy Butson 2024 based on UWA CITS2401 Lecture Notes

# Basics and Style
The shell covers a kernel and allows interacting with a user's input

**REPL** = Read Evaluate Print Loop

Operator precedence does occur, follows BIDMAS rules

```python
'''
this is code with various reminders and functions.
Written by Jeremy Butson 25/02/24
'''

import yadayada

phone_number = "0478634195"
print(phone_number[::-1])                          #reverses phone number

sum([1, 2, 3])                                     #returns 6

locals()                                           #returns current vars

int(3.4) == 3
float(2) == 2.0
complex(4.5) == 4.5 + 0j

round(6.433421) == 6
abs(-3) == 3
int("67") == 67
```

## DATA TYPES:
- Integers (123)
- Float (0.00)
- Complex (5+2j)
- String ("hello")
- Boolean (True/False)
```python
type(123)                           #returns int
```

## OPERATORS:
 - > < == <= >= != + - / // % * ** += -=

## DEFINING FUNCTIONS:
```python
def square(x):
	"""squares a number"""    #called a docstring, explains what function does
	return x*x
```

## STYLE
- programming should be *correct, readable and maintainable*
- will be using PEP8
	- peps.python.org/pep-0008/
	- ### [A Foolish Consistency is the Hobgoblin of Little Minds](https://peps.python.org/pep-0008/#a-foolish-consistency-is-the-hobgoblin-of-little-minds)
- for wide-scope variables: use only lower case, separating words with __ 
	- use clear variable names (not just x or y etc.)
- break into lots of single usage functions
- don't use global variables
- at most 40 lines per function
- at most 4 levels of indentation
- use library functions when possible
- use a main() statement to  start code
- use ALL_CAPS to define a global constant at the top of program
- separate functions 2-3 blank lines
- use white-space around o p e r a n d s
- every program must have a *docstring* at the top stating
	- author
	- role
	- date
- every function must have a *function docstring* saying what it does
	- this should be *after* the function definition
- otherwise use #comments sparingly

## Taking Inputs:
```python
name = input("Please enter your name: ")
print("HELLO " + name + "!")
```

# Strings & Lists
A **string** is a sequence of characters.
A **literal** is a constant.

## STRINGS:
- Can be shown using:
	- "..."
	- '...'
	- '''...''' or """..."""
```python
print("Hello", end = '\n')             #default (new line character)
print("Hello", end = '')              #make it so it doesn't go to new line
```
- Best delimiter to use:
	- Recommended to use "..." unless the string contains those characters
	- Hence where '''...''' comes into use
	- OR "\\"Hello\\""
- Triple quotes does NOT end a string with new line, or when a backslash precedes the new line (escape)
- **STRING OPERANDS:**
	- '+' adds two strings together (concatenation)                                 str() + str()
	- '\*' multiplies a string by a given number (repetition)
	- '%' performs string formatting 

## CALLING METHODS:
```python
objectName.methodName()

#i.e. 
name.find('x')

#Common String Methods:
capitalize()                                  #capitalises first letter
find(substring [, begin [, end]])
lower()
upper()
strip([charsToStrip])
startswith(prefix [, start [, end]])           #similarly for ends with
split([delimiter])
format(value [, value])

#f-String Basics:
name = "James"
height = "189.3"
print(f"Name: {name}, height: {height})
#f-String also takes away new line character
str = "a"
print(f"{str:>10}")                            #justifies 10 spaces to right
string.strip()                         #default gets rid of blank spaces
```


## LISTS:
- A list is a sequence of objects
- list\[0] gets the first item
- Index starts at 0
- `len()` produces number of items in list
- list\[-1] accesses last item
- List object is just a list of references
- List objects are mutable
- We can get slices, or SUBLISTS:
	- `print(listName[start:end+1])`
- **OPERATORS & METHODS:**
	- `list + list2` concatenates list
	- `3 in [1,2,5]` is false
	- `3 * list` repeats list 3 times
	- `len(list)` number of items
	- `sum(list)` adds them up
	- `min(list)` and `max(list)`
	- Also:
	  `list.append(object) , list.count(value) , list.extend(list2) , list.index(value) , list.insert(index, object) , list.pop([index]) , list.remove(value) , list.reverse() , list.sort() , list("String") = ['S', 'T', ...] list(range(1,3)) = [1, 2, 3]`
	- Use slicing to make a copy of a list:
		`list2 = list[:]`

## TUPLES:
- **Tuples** are like lists but with parenthesis instead of brackets
- Tuples are immutable 

# Loops & Nesting
**Definite Loop**: for loop
```python
for i in [0,1,2,3,4]:
	i_sqr = i * i
	print(f"{i} squared = {i_sqr:2}")

(i * i) for i in [0,1,2,3,4]                        #returns the same
```
- Programming patterns for solving common problems:
	- accumulator
	- mapped-list (get a function of every value)
	- counting-loop
		- `for i in range(0, 7, 2):`
	- updated-list

**Indefinite Loop**: while loop


## NESTING:
- Something within something
```python
rainfalls = [
	[0,1,2,3],
	[4,5,6,7],
	[8,9,1,2]
]
```
- Need a nested loop in order to print this whole table: go through each row and print each column in each row

# Conditions
## Booleans:
- Either ``True`` or ``False``
- Using signs ``< > <= >= == !=``
	- Notice ``=`` is an assignment function, ``==`` is a comparative
- Also returns from ``startsWith`` etc.
- use ``is_condition`` when naming Booleans

## ``If`` Statements:
```python
if boolExpression:
	block
elif boolExpression2:
	block
else:
	block
```
- NEVER compare floats for equality (cannot be guaranteed)

## Logics:
- Lazy evaluation:
	- a or b returns True if a is True; only evaluates b if a is False
	- a and b returns False if a is False; evaluates b only if a is True
	- Important if b has side effects or could generate an error
- Avoid complex logic by:
	- Simplifying logical expressions (de Morgan's, etc.)
		- ``not (a or b)`` is equal to ``not a and not b``
	- Flattening nested code
	- Introducing temporary Boolean variables
	- Writing Boolean-valued functions

## ``while`` Loops:
```python
while condition:
	statementBlock
```
- Sometimes we do not have a known sequence so must use while loops instead of for loops
- Need to make sure that the loop condition will eventually come true, otherwise the program loops forever (infinite loop)
- There are also input condition while loops:
	- For example: looping until a use presses quit
- ``break`` forces an immediate exit from the loop, goes straight to first statement after the loop
- ``continue`` will only skip the current iteration

# Functions
## Modules
- Control complexity, large programs broken down into functions
- As they get larger, broken into modules, these are usually in separate files
- The Python library is a large collection of modules
- `import some_module`
	- This loads **and executes** the file some_module.py
- Some common modules:
	- `math`
		- `math.pi` `math.sqrt()` etc.
		- You can select specific functions:
			- `from math import pi, sqrt`
- When you run a program, its `__name__ == __main__`
- When you ask a module for its ``__name__`` it is the module files name
	- This can be used in testing modules:
		- `if __name__ == '__main__':` as it will only run if you are running the program directly not if its being used as a module

## Parameters
- **Default parameters** allow functions to be called with different numbers of arguments
	- This reduces code repetition and helps to do one job well
	- ``def find_first(item, data, start_index = 0):`` 
		- `start_index` is a default parameter
	- Parameters without defaults *MUST* come first
- **Variable parameters** are functions that receive *any* number of arguments
	- e.g. function `max()` is: `ourMax(first, *rest):` where `*rest` is a tuple
- **Keyword arguments**: 
	- if you do not know the order:
		- for function ``def describe(age, name):`` if the user does not know the order they can instead call it with ``describe(name = "jeremy", age = 20)

## Functional Decomposition
- Is the code readable and maintainable?
- Functional decomposition to increase clarity and avoid repetition
- Reasons for functions:
	- to make code easier to understand
	- to make code reusable
- 2 sorts of functions:
	- Procedures: don't return a value to the caller, do print or write etc., name starts with a verb
	- Real functions: does return a value to the caller, names are nouns
- Functions arise:
	- Deliberately, from top-down design
	- During refactoring when cleaning up code
- Extracting a function:
	- Any sequence of complete statements can always be pulled out into a separate function by:
		- identifying all variables that must be defined already
		- identifying all variables that get defined or altered by the statements or are needed later

# Files & Exceptions
>Specifically focused on reading files for data and statistics

## Files as Sequences
- Built in function `open(path[, mode])`
- `path` is a *filepath* string, and uses forward-slashes instead of backslashes
- `mode` is `r w a` for reading, writing and appending
- A *file object* is a sequence of lines
```python
data = open("junk.txt")
for line in data:
	print(line[0:-1])
data.close()

#OR (but this uses more memory)

data = open("junk.txt")
lines = data.readlines()
for line in lines:
	print(line[0:-1])
data.close() 
```
- We can also access internet resources as files:
```python
import urllib.request

url = "http://web.csse.uwa.edu.au"
web_page = urllib.request.urlopen(url)
for line in web_page:
	print(line)
web_page.close()
```

## Example Reading of Data
```python
infile = open("lect07a_bubble.txt)

bubbles = []
for line in infile:
	data = line.split()    #the data is split by spaces
	bubble = float(data[3])
	bubbles.append(bubble)

print(sum(bubbles)/len(bubbles))
infile.close()

######################################################################
lect07a_bubble.txt:
######################################################################
1 1 2 53
3 4 5 60
2 3 5 43
```

## Extracting Data
- Need to make sure that you get the data that is actually needed, skipping any unnecessary file data
```python
while line != '\n':
	pieces = line.split(',')
	date = piece[2:5]
	if pieces[5] != null:
		rainfall = float(pieces[5])
```

## Writing Files
```python
out_file = open('myoutput.txt', 'w')               #create new file
data = "{0}, {1}, {2}, {2:.3f}\n"                  #explicitly us \n
out_file.write(data)
out_file.close()
```

## Debugging and Exceptions
- We want a program to continue doing other things if some non-breaking thing goes wrong
- We know that these things might happen, however we do not know when
- We can use `if` conditions or functions, however this is tedious and you may miss some errors
- Hence we use an exception:
```python
def print_reciprocal(n):
	try:
		recip = 1.0 / n
		print("Reciprocal of ", n, " is ", recip)
	except:
		print(n, " does not have a reciprocal)
```
- Exceptions allow us to separate normal from exceptional code
- The except block is only processed if an exception occurs
- However, we usually want to use for specific exceptions (better formatting and output)
```python
def print_reciprocal(n):
	try:
		recip = 1/n
	except TypeError:
		print("parameter must be a number")
	except ZeroDivisionError:
		print("reciprocal of zero is undefined")
	else:
		print("Reciprocal is ", recip)
```
- Always use boundary cases when testing to ensure that things haven't "slipped through"

# Sets & Dictionaries
- Lists are mutable \[  ,  ]
- Tuples are immutable (  ,  )

## Sets
- Collections of unordered and distinct items
- Sets are mutable, but items are immutable
`farm_animals = set(["goat", "pig"])`
- set() is faster than just creating a list
	- This is because it uses a hash function to check whether something is in a list, time of O(1)
- Methods:
```python
.add()
.remove()
.clear()
set1.union(set2)
set1.intersection(set2)
set1.difference(set2)
set1.symmetric_difference(set2)       #finds the XOR
set1.issubset(set2)
set1.issuperset(set2)
```
- To create sets of sets we must make the items in the sets immutable, so we use `frozenset()`

## Dictionaries
- Key and value pairs
- `fruit_counts = {'banana' : 3, 'apple' : 1, 'pear' : 7}`
- Type name is `dict`
- Methods:
```python
#adding
fruit_counts['mango'] = 42

#deleting
del fruit_counts['apple']
fruit_counts.pop('apple')

#clear
dict.clear()

#get value associated with key
fruit_counts.get('apple')

#get a list of the keys
fruit_counts.keys()

#get list of key/value pairs
fruit_counts.items()

#get list of values
fruit_counts.values()

#add a set of key/value pairs to the dictionary
fruit_counts.update(set)
```

# Objects
#### Class
A user-defined prototype for an object that defines a set of attributes that characterise any object of the class
**Class Definition Example**:
```python
class Colour:
	"""An empty class --- all it has is a name"""
	def __init__(self, red, green, blue):
		"""Initialisation, defining its instance variables"""
		self.red = red
		self.green = green
		self.blue = blue

def display(Colour):
	"""function to print a given colour"""
	print(f"(r:{colour.red}, g:{colour.green}, b:{colour.blue})")

colour = Colour(255, 123, 53)
display(colour)
```

#### OOP Inheritance and Polymorphism
**OOP** is Object Oriented Programming (all our code is in classes)
```python
class Point:
	"""A point in 2-space"""
	def __init__(self, x, y):
		"""The INITIALISER"""
		self.x = x
		self.y = y
	def __str__(self):
		"""returns string representation"""
		return f"(x-coord: {self.x})

p1 = Point(10, 20)
print(f"The x-coord of p1 is {p1.x}")
```
**Polymorphism** is the ability of a bit of code to handle different data types

#### Rectangle Example
```python
class Rectangle:
    """Rectangle object that can find its area and perimeter"""
    def __init__(self,width=1, height=2):
        self.width = width
        self.height = height
    def area(self):
        """calculates area of a rectangle object"""
        width = self.width
        height = self.height
        area = width * height
        return area
    def perimeter(self):
        """calculates area of a rectangle object"""
        width = self.width
        height = self.height
        perimeter = 2 * width + 2 * height
        return perimeter

my_rec = Rectangle()
print(my_rec.perimeter())
```

# NumPy
**NumPy** is the fundamental package for scientific computing with Python

#### Arrays
- All elements are of the same type
- they are multidimensional
- Arrays are fast because they are normally laid out sequentially in memory
```python
import numpy as np

array1 = np.array([0, 1, 2, 3])
array2 = np.array([1, 2, 3, 4], dtype = float)
matrix = np.array([[3, 5],
				   [7, 9],
				   [3, 6]])
print(array1[2])
print(matrix[1, 2])
matrix[0][1] = 1
print(array1[0:2])

#===============================
people = np.array([
				   ("Alice", 25, 158.2)
				   ("Bob", 43, 173.1)
				], dtype = [("name", "U10"), ("age", int), ("height", float)])

print(people[0])
people[0] = ("Leon S Kennedy", 32, 184.2)
print(people[0]["name"])
print(people[np.where(people["age"] < 40)
```

#### NumPy Loops
**Problem**: Find the lowest value of $\theta$ between 0 and pi, where the function $f(\theta)$ crosses the x-axis:
	$f(\theta) = cos(2\theta + \pi / 8) + sin(3\theta + \pi/6)$
```python
import numpy as npp
import math
import matplotlib.pyplot as plt

SKIP = 0.01

def crossing(value):
	return np.cos(2 * value + math.pi / 8) + \
		   np.sin(3 * value + math.pi / 6)

def main():
	value = 0
	last_val = crossing(value)
	while value <= math.pi:
		value += SKIP
		currentCos = crossing(value)
		plt.plot([value], [currentCos], "g.")
		if (currentCos * last_val) <= 0:
			print("x crossing near angle ", value - SKIP)
		last_val = currentCos
	plt.show()
```

#### NumPy Functions
```python
z = np.zeros([4, 4]) #create an array of size 4 x 4 of zeroes
a = np.ones([3, 3])
b = np.eye([2, 2]) #identity matrix

c = np.arange(2, 9, 3) #ranged array from 2 - 8, stepped by 3
d = np.linspace(10.0, 20.0, 5) #start, end, number of values between

# FUNCTIONS FOR SUMMARISING
np.count_nonzero(array1 >= 10) #non-zero and matches conditions
np.all(array1 == 9) #whether all records match conditions
np.any(array1 == 9) #if any records match
np.sum(array1)
np.amin(array1)
np.amax(array1)
array1.T #transposes the array
np.sort(array1)
-np.ssort(-data) #sort in descending
np.save("my_rainfall_data", rainfall) #saves where rainfall is the array
back_again = np.load("my_rainfall_data.npy")
np.savetxt("rainfall.csv", rainfall, delimiter = ",")
back_again = np.loadtxt("rainfall.csv", delimiter = ",")

# Algebra
array1.dot(array2) #finds dot product
array1_sqaured = matrix_power(array1, 2)
array1_inverse = matrix_power(array1, -1) or = inv(array1)
```

# SymPy
- SymPy is used for applying symbolic computation techniques to areas such as algebra.
- Variables in SymPy must be declared
```python
from sympy import symbols, diff

x, y = symbols('x y')
y = x ** 2
diff(y)                  #returns 2x
```

#### Displaying Formulas
```python
>>> from sympy import init_session
>>> init_session()
>>> #insert sympy formula to be displayed
```

#### Solving
```python
from sympy.solvers import solve
from sympy import symbols

solve(x**2 + 4*x + 3, x)              #returns [-3, -1]

x, y, z = symbols('x y z')
solve([z-4*x,
	  x-y,
	  z-(x**2+y**2)])   #solves the system of equations

simplify(equation)
equation.subs(x, 1) #substitutes x for 1
equation.subs([(x, 3), (y, 4)])
```


# Pandas
- Open source data analysis and manipulation tool
- `python3 -m pip install pandas`
```python
import pandas as pd
df = pd.read_csv('csv_fille.csv')
df.head(10)        #view first 10 rows
df.describe()      #shows basic stats for each column
df.info()          #content of the data type in each col

###DISPLAY OPTIONS###
pd.set_options('display.max_rows', 500)
pd.set_options('display.width', 1000)

write_html("demo.html",
		  df.head(10).style.\
		  highlight_max(color='darkgreen').\
		  highlight_min(color='#ff0000'))
```

# Visualisation
#### Graphical Output
- We will be using `matplotlib` as it is:
	- Multiplatform
	- Publication-quality output 
	- Extremely flexible

#### Plotting with Matplotlib
```python
import matplotlib.pyplot as plt

plt.plot([1,2,3,4], [1,4,9,16], "gx"   #first series (in green, using x marks)
		[1,2,3,4], [2,3,10,15], "r-")  #second series (in red, using a line)
plt.legend(['line 1', 'line 2'])
plt.title('Title of Graph')
plt.ylabel('some numbers')
plt.show()

#using a dataset:
import pandas as pd
df = pd.read_csv('temporal.csv')
plt.xticks(range(0, len(df['Mes']), skip), df['Mes'][:: skip], rotation=90)
plt.tight_layout() #to see x-axis
plt.plot(df['data science'])

#loops
import math
x = 0.0
while x < 4 * math.pi:
	x = x * 0.05
	y = math.sin(x)
	plt.plot([x], [y], 'r.')
	if y <= 0:
		continue
	plt.plot([x], [y*2], 'g.')
plt.show()

#subplots (putting two graphs next two each other)
plt.sublot(int rows, int cols, int loc)
#put second graph calcs here
```

#### Interpolation
- Linear interpolation assumes that data follows a straight line between adjacent measurements
`numpy.interp(x, xp, fp)`
- Cubic spline interpolation is made up of segments of cubic polynomials
```python
import numpy as np
from scipy import interpolate
```

#### 3D Plotting
- Can be done using `matplotlib`
- need to `from mpl_toolkits.myplot3d import Axes3D`

#### Curve Fitting
- Used when we want to match an analytical (or symbolic) model to a set of measurements which may contain some error
- One method is linear regression:
```python
pol = numpy.polyfit(x, y, degree)
x_val = np.linspace(0, 6, 100)
y_val = numpy.polyval(pol, x_val)
```

# Advanced NumPy
#### Array Broadcasting
- Allows you to perform operations on arrays with different shapes
```python
import numpy as np
#allows you to perform operations on arrays with different shapes
x = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
y = np.array([1, 0, -1])
#We can use broadcasting to add y to each row of x as follows:
print(x)
result = x + y.reshape(3, 1)
print(result)
```
- Broadcasting can be used to perform operations on arrays with different dimensions
```python
x = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
a = 2
result = a * x
print(result) [[ 2 4 6 8]
				[10 12 14 16]
				[18 20 22 24]]
```

#### Universal Functions `ufunc`
- Allows efficient element-wise operations on arrays without the need for loops or element-by-element operations
- Allows us to just `C = A + B` arrays, instead of having to loop through the arrays

