# Basics Content
## Syntax
```py
print ("Hello world")
```
## Var and Data types 
```py
# Number: Int and Float 
myint = 7
myfloat1 = 7.0
myfloat2 = float(7)

# String
mystring = "hello world"

# Lists ( very simiar to arrays)
mylist = []
mylist.append(1)
mylist.append(2)
## list travelsal
for x in mylist:
  print(x)
```
## Basic Operations
- Arithmetic Operators: + - * / % **
- Using operators with Strings
- Using operators with Lists

## String formating
`s`% - String (or any object with a string representation, like numbers)
`%d `- Integers
`%f` - Floating point numbers
`%.<number of digits>f` - Floating point numbers with a fixed amount of digits to the right of the dot.
`%x/%X` - Integers in hex representation (lowercase/uppercase)

## Basic string operation
```py
astring = "Hello world"
print(len(astring))
print(astring.index("o"))
print(astring.count("l"))
print(astring[3:7])
print(astring[3:7:1]) # string[start, stop, step]
print(astring[::-1]) # reverse
print(astring[upper()])
print(astring[lower()])
print(astring.startswith("Hello")) # boolean
print(astring.endswith("world")) # boolean
print(astring.split(" ")) # str > ["str1","str2"]
```
## Condition

## Conditionals and Loop
### Conditionals
#### Syntax
```py
x = 2
if x == 2: 
  print ("x equals 2")
elif x != 2:
  print ("x not equals 2")
else: print ("dont have else case ok")
```
#### Operator
- Operator: = == != > < 
- Boolean operator: and or
- `in` operator
``` py
name = "Nguyen"
listNames = ["Nguyen", "Khoi"]
if name in listNames:
  print("name is in lists")
```
- `is` operator
```py
x = [1,2,3]
y = [1,2,3]
z = x
print(x == y) # Prints out True
print(x is y) # Prints out False
print(z is x) # Prints out True
```
- `not` operator
```py
print (not False) # prints out true
```
### Loops
- The `for` loop
## Type Casting
## Exceptions
## Funtions, Builtin Function
## Lists && Tupes && Sets
## Dictionaries
