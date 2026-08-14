# Bash

* Scripting language.
* Imperative language.
* Non-typed & mutable variables.
  
**CONTENTS**

- [Bash](#bash)
  - [Help \& manuals](#help--manuals)
  - [Variables](#variables)
    - [Pre-defined variables](#pre-defined-variables)
    - [Environment variables](#environment-variables)
    - [String variables \& modifications](#string-variables--modifications)
  - [Array variables](#array-variables)
  - [Brace expansion](#brace-expansion)
  - [Coding structures](#coding-structures)
    - [Loops](#loops)
    - [Conditionals](#conditionals)
  - [Input/Output](#inputoutput)


## Help & manuals
WIP

## Variables
In bash the variables can store numbers or strings. Here there are the basic usage/facts:

* **For declaring a variable**, use `var="a"`. If you put some space between the equal sign, it will be erroneous. The variables are **mutable**.

* The variable names are **case-sensitive**.

* Can use **local variables** in functions with `local`. Also, we can define constant variables with **readonly $VAR** and unset a variable with **unset $VAR**

* The variables can be used only inside double quotes (`""`), the single quotes (`''`) doesn't expand the variables values. 

* The variables can be used with `${var_name}` (called *paramenter expansion*), wich means that the variable is printed or modified. 

  We should use the expansion syntax for define default values, with `"${foo:-"DefaultValue"}"`. 
  The default value is used if foo is:
  * a null variable `(foo=)` 
  * a empty string `foo=""`.

### Pre-defined variables
There are some pre-defined variables:

|Variable | Explanation |
|-------|------|
|`$?`| Last return value|
|`$$`|Current PID |
|`$#`| Number of args passed to the script |
|`$@`| All args passed to the script |
|`$1 $2...$n`|i-th argument of the script |

### Environment variables
This special kind of variables are defined for all child shells in the systems. Can be defined using `export var=value`.

### String variables & modifications
The strings variables have defined builtins, using the expansion syntax for make common operations like:
* String substitution (**first apparence only**) : `${var/old/new}`
* String lenght: `${#var}`
* Substring from a variable

## Array variables

To declare an array we use the parenthesis, `arr=(one two 4 56 7)`. 

`$Arr` only point to the first element, for accessing elements again is required to use the *expansion* syntax.

* Access i-elements (starting from 0): 
* Access i-elements backward (starting from -1):
* Get all elements : 
* Get number of elements:


## Brace expansion
Used to generate arbitrary strings


## Coding structures

### Loops 

### Conditionals
 
## Input/Output

