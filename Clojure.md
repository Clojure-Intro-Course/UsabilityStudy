
## Brief Overview of Clojure

This is a very brief overview of a subset of Clojure features for those familiar with the Racket programming language. It is intended for a usability study at UMM and assumes a non-standard Clojure environment. 

### How to run a Clojure program
Note: the instrcutions are specific to this usability study. 

*TO-DO*: instructions. 

### Syntax
Just like Racket, Clojure follows the prefix notation: `(function arg1 arg2...)`. A lot of functions on numbers have the same names as in Racket, so all of the following is valid in Clojure as well. Comments are also the same: `;`. 
```clojure 
(+ 1 2 3 4) ; returns 10
(even? 2) ; returns true
(<= 4 3) ; returns false
```
TO-DO: println (since the tests will run using println). 

### Defining variables and functions
Functions and variable defintions are somewhat different from those in Racket. Variables are defined using the `def` keyword, instead of Racket's `define`:
```clojure 
(def n 5)
(+ n 5) ; results in 10
```
Just like in Racket, variables are immutable: once defined, their value cannot be changed.

Functions are defined using the `defn` keyword. The function parameters are included in square brackets after the function name (no commas), and the body of the function is after the closing bracket. The entire `defn` expression is surrounded by parentheses:
```clojure 
; A function of one argument:
(defn add2 [x]
  (+ x 2))

(add2 5) ; results in 7

; A function of two arguments
(defn sum-squares [x y]
  (+ (* x x) (* y y)))

(sum-squares -1 2) ; results in 5
```
Just like in Racket, variable and function names may contain letters, digits, dashes, some punctuation symbols (`?` and `!`). The names are case-sensitive. 

### Common functions 

### Conditionals: 'if', 'cond', and combining conditions

### Hashmaps 

### Lists and common lists functions

### nil

### Recursion on lists

### map, reduce, and similar functions on lists

### Anonymous functions 
