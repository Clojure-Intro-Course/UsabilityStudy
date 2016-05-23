
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

See documentation on [def](https://clojuredocs.org/clojure.core/def) and [defn](https://clojuredocs.org/clojure.core/defn)

### Common functions 
Many functions on numbers are the the same in Clojure and Racket. This includes most of arithmetic operations, comparisons, and predicates: 
```clojure 
;; common functions on numbers
(+ 2 3) ; results in 5
(* 2 3 4) ; results in 24
;; predicates (functions that return true/false) often end with ?
(even? 3) ; results in false
(odd? 3) ; results in true
```
Clojure uses `inc` for "increment" function (the same as `add1` in Racket) and `dec` for "decrement" (the same as `sub1` in Racket):
```clojure 
(inc 5) ; results in 6
(dec 5) ;results in 4
```
See documentation for [numeric functions](https://clojuredocs.org/quickref#numbers).

### Conditionals: 'if', 'cond', and combining conditions
Conditions in Clojure are very similar to those in Racket. For instance, `if` looks identical to that in Racket:
```clojure 
(def n 5)
(if (< n 10) 2 3) ; results in 2
(if (< n 2) 2 3)  ; returns 3
```
However, there is a difference in how Clojure and Racket determine if a value is true or false. In Racket the expression in the condition of `if` must evaluate to a boolean (true or false). In Clojure any result other than `false` and `nil` (that is covered later in this overview) is considered to be true. For instance, any number (including 0) is considered to be true:
```clojure 
(if 5 "yes" "no") ; results in "yes"
(if 0 "yes" "no") ; also results in "yes"
```
See documentation on [if](https://clojuredocs.org/clojure.core/if).

`cond` is also very similar to Racket (and just like `if`, it interprets any non-false and non-nil value as true). A slight difference is that the final `else` case of `cond` is written as `:else`.  - THIS IS ACTUALLY NOT TRUE (different syntax)
```clojure 
(cond
  (< n 5) "apple"
  (> n 5) "banana"
  :else "orange")
```
See documentation on [cond](https://clojuredocs.org/clojure.core/cond).

```clojure 

```

### Hashmaps 

### Lists and common lists functions

### nil

### Recursion on lists

### map, reduce, and similar functions on lists

### Anonymous functions 
