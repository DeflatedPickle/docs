# Koi In Action

## Comments

Like most languages, comments can be made in Koi, that will be ignored by the interpreter/compiler. Comments are created with a number sign.

```text
# I'm a comment
```

Multi-line comments can also be created, starting with a number sign then a dash and finishing with a dash then a number sign.

```text
#- 
   I'm
   a multi-line
   comment
-#
```

## Types

* Boolean - A value that can be on or off
* Integer - A whole number
* Float - A floating point number
* Double - A double precise float
* Character - A single character
* String - An array of characters
* Array - An amount of the same type of value

### Collections

* List - A sorted amount of different types of values
* Tuple - An immutable sorted amount of different types of values
* Set - A set of values, where a value may only be used once
* Dictionary - A set of key/value pairs of data

#### Examples:

```text
var integer: int = 0
# Or
var integer := 0

###

var integer_list: int[] = [0, 1, 2] # Integer only list
# Or
var integer_list := [0, 1, 2] # Integer only list

var generic_list: list = [0, "1", 2] # Object list (any type)
# Or
var generic_list := [0, "1", 2] # Object list (any type)

###

var integer_tuple: int() = (0, 1, 2) # Integer only tuple
# Or
var integer_tuple := (0, 1, 2) # Integer only tuple

var generic_tuple: tuple = (0, "1", 2) # Object tuple (any type)
# Or
var generic_tuple := (0, "1", 2) # Object tuple (any type)

###

var integer_dict: int{} = {"0": 0, "1": 1, "2": 2} # Integer only set
# Or
var integer_dict := {"0": 0, "1": 1, "2": 2} # Integer only set

var generic_dict: dict = {"0": 0, "1": "1", "2": 2} # Object set (any type)
# Or
var generic_dict := {"0": 0, "1": "1", "2": 2} # Object set (any type)

###

var integer_set: int<> = <0, 1, 2> # Integer only set
# Or
var integer_set := <0, 1, 2> # Integer only set

var generic_set: set = <0, "1", 2> # Object set (any type)
# Or
var generic_set := <0, "1", 2> # Object set (any type)
```

The length of the list, tuple or set can be specified by putting the number between the brackets. If a length is not specified, the list will be dynamically sized.

```text
var integer_list: int[3] = [0, 1, 2]
# var integer_list: int[3] = [0, 1, 2, 3] # Error - list contains more than 3 items
```

## Sub-Routines

All of the sub-routines can be called like so:

```text
{id}({parameters*})
```

### Subroutine

A subroutine is a function that works in the global scope. Because of this, they do not accept parameters.

```text
sub {name} {block}
sub {name} -> {type} {block}
```

#### Example:

```text
var my_var := 3

sub mySub {
    my_var += 3
}

# Prints 3
print(my_var)

mySub()

# Prints 6
print(my_var)
```

### Procedures

A procedure is a function that does not have a return value. Procedures lack the ability to return anything, so an error will be raised if a variable is assigned to a procedure call.

```text
pro {name}({parameters*}) {block}
```

#### Example:

```text
var my_var := 3

pro myPro(v) {
    print(v + 3)
}

# Prints 6
myPro(my_var)
```

### Functions

A function can be called with a defined set of parameters. The parameter names, types and optional values are defined with the functions and the values are defined when the function is called. If the return type is not specified, it will be "none".

```text
fun {name}({parameters*}) {block}
fun {name}({parameters*}) -> {type} {block}
```

#### Example:

```text
var my_var := 3

fun myFun(v) {
    return v + 3
}

# Prints 6
print(myFun(my_var))
```

### Methods

A method is a function that belongs to a class, they have their own scope but can also work with the class scope.

```text
meth {name}({parameters*}) {block}
meth {name}({parameters*}) -> {type} {block}
```

### Parameters

Parameters are used in sub-routine declaration and are then used from the sub-routine. The type and default value of a parameter are optional.

The most basic form of a parameter is just an ID.

```text
{id}
```

#### Example:

```text
fun myFun(v) {
    return v + 3
}
```

However, the type of the parameter may also be specified.

```text
{id}: {type}
```

#### Example:

```text
fun myFun(v: int) {
    return v + 3
}
```

A default value for the parameter can be defined, either on its' own or with the type.

```text
{id} := {default value}
{id}: {type} = {default value}
```

#### Example:

```text
fun myFun(v := 3) {
    return v + 3
}

fun myFun(v: int = 3) {
    return v + 3
}
```

The last parameter may also have an ellipsis after the ID, making that parameter into a list of the given type. The parameter will now no longer be able to accept a default value. The function call will now accept an endless amount of values, with the extra values being passed into the parameter with an ellipsis.

```text
{id}...
{id}: {type}...
```

#### Example:

```text
fun myFun(v: int...) {
    vs: int[] = []

    for i in v {
        vs.append(i + 3)
    }
    
    return vs
}
```

### Calling

To call a sub-routine, simply type the name of the function, and then a pair of parenthesis. Inside the parenthesis, place each parameter value or parameter name and value that the sub-routine accepts.

```text
fun myFun(v: int) {
    return v + 3
}

print(myFun(3))
```

## Classes

Classes are objects that can contain variables and methods. Classes can be extended from other classes, carrying over the extended classes' variables and methods. Methods from the extended classes' can then be overridden in the new class.

```text
class MyClass({extensions*}) {block}
```

## Variables

Variables are names that are attached to values. The variables available depend on the current scope. Variables can be defined as mutable with "`var`" or as final with "`val`".

```text
var my_var: {type} = {value}
val my_val: {type} = {value}
```

The value of the variable is optional, if not specified, it will be "none" or the smallest it could be for the specified type - 0 for an integer. The type, however, must either be specified or the following syntax must be used:

```text
var my_var := {value}
val my_val := {value}
```

## Properties

A property is like a variable, though they have easy getters and setters.

```text
prop my_prop: str = "hello, " {
    getter { return me + "world" }
    setter(value: str) { me = value }
}

# Prints "hello, world"
println(my_prop)
```

## Statements

### If

An if statement is used to compare values with others. An if statement can optionally be followed by an elf and/or else statements.

```text
if {boolean} {}
```

### **Elf**

An elf statement can only follow an if statement, and is run if the comparison in the if statement is false, but its' comparison is true.

```text
if ... {}
elf {boolean} {}
```

### **Else**

An else statement can only follow an if or elf statement, and is run if the comparison in the if or elf statements were false.

```text
if ... {}
else {}

if ... {}
elf ... {}
else {}
```

## Loops

### For

For loops will loop for as long as there is another item in the given object with length, the value of the given id will be set to the value of the current item in the object with length.

```text
for {id} in {object with length} {}
```

For loops can also be used to loop through multiple things, using commas for each loop. If one of the objects with length is longer than the other, the id for the shorter one will become null after all items have been looped through.

```text
for {id} in {object with length}, {id} in {object with length} {}
```

### While

A while loop will loop for as long as the comparison is true. As soon as it isn't, the loop will stop.

```text
while {boolean} {}
```

## Operators

### Comparison

Comparison operators can be used to compare two values and return a boolean.

```text
{value} {comparison operator} {value}
```

### Arithmetic

Arithmetic operators are used to perform mathematical functions on values.

```text
{value} {arithmetic operator} {value}
```

