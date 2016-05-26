<!-- TOC depthFrom:2 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Brief Overview of Clojure](#brief-overview-of-clojure)
	- [How to run a Clojure program](#how-to-run-a-clojure-program)
	- [Syntax](#syntax)
	- [Defining variables and functions](#defining-variables-and-functions)
	- [Common functions](#common-functions)
	- [Conditionals: 'if', 'cond', and combining conditions](#conditionals-if-cond-and-combining-conditions)
	- [nil](#nil)
	- [Hashmaps](#hashmaps)
	- [Lists and common list functions](#lists-and-common-list-functions)
	- [Recursion on lists](#recursion-on-lists)
	- [map, reduce, and similar functions on lists](#map-reduce-and-similar-functions-on-lists)
	- [Anonymous functions](#anonymous-functions)

<!-- /TOC -->
## Brief Overview of Clojure

This is a very brief overview of a subset of Clojure features for those familiar with the Racket programming language. It is intended for a usability study at UMM and assumes a non-standard Clojure environment.


### How to run a Clojure program
Note: the instructions are specific to this usability study.

You will have a LightTable file open and a terminal (command prompt) window open. The name of the file will be `test.clj` for our error messages and `test_standard.clj` for the standard Clojure error messages (you will be working with either our messages or the standard ones). 

Copy your code into the file where indicated. Don't forget to save the file (Ctrl-S). In the terminal window type `lein run` for our error messages or `lein run s` for standard ones (after you type the command the first time, you can use "up" arrow and "enter" to run it again). 

There will be a long list of warning displayed in the terminal, ignore those. Your output starts with a line of `******`. If no error happens, it ends with the word `Done`. 

### Syntax
Just like Racket, Clojure follows the prefix notation: `(function arg1 arg2...)`. A lot of functions on numbers have the same names as in Racket, so all of the following is valid in Clojure as well. Comments are also the same: `;`.
```clojure
(+ 1 2 3 4) ; returns 10
(even? 2) ; returns true
(<= 4 3) ; returns false
```
In order to display information from your program, you need to use the function `println` (stands for "print line"):
```clojure
(println "Hello") ; prints "Hello", returns nil
```
All of the tests given to you are included in `println`. If you want to add your own or display intermediate results, make sure to include them in `println`. 

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
Just like in Racket, variable and function names may contain letters, digits, dashes, and some punctuation symbols (`?` and `!`). The names are case-sensitive.

See documentation on [def](https://clojuredocs.org/clojure.core/def) and [defn](https://clojuredocs.org/clojure.core/defn)


### Common functions
Many functions on numbers are the the same in Clojure and Racket. This includes most arithmetic operations, comparisons, and predicates:
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

The length of a string is computed using the function `count`:
```clojure
(count "abc") ; results in 3
```


### Conditionals: 'if', 'cond', and combining conditions
Conditions in Clojure are very similar to those in Racket. For instance, `if` looks identical to that in Racket:
```clojure
(def n 5)
(if (< n 10) 2 3) ; results in 2
(if (< n 2) 2 3)  ; returns 3
```
However, there is a difference in how Clojure and Racket determine if a value is true or false. In Racket the expression in the condition of `if` must evaluate to a boolean (true or false). In Clojure any result other than `false` or `nil` (that is covered later in this overview) is considered to be true. For instance, any number (including 0) is considered to be true:
```clojure
(if 5 "yes" "no") ; results in "yes"
(if 0 "yes" "no") ; also results in "yes"
```
See documentation on [if](https://clojuredocs.org/clojure.core/if).

`cond` is also similar to Racket. However, it doesn't have brackets around each case: `cond` keyword is followed by pairs in which the first element is a condition, and the second is the resulting value if that condition is true. Just like in Racket, the else clause is optional. If it is given, it is indicated by `:else` (note the colon in the front). In the example below, if `n` is less than 5 then "apple" is returned, if it's greater than 5 then "banana" is returned, and in the remaining case (`n` equals to 5) "orange" is returned.
```clojure
(cond
  (< n 5) "apple"
  (> n 5) "banana"
  :else "orange")
```
Recall that `cond` in Racket fails when none of the cases match and there is no `else` case. Unlike Racket, Clojure `cond` returns `nil` if none of the cases match:
```clojure
(cond 
  (> 2 3) "yes" 
  (> 3 4) "no") ; results in nil
```

See documentation on [cond](https://clojuredocs.org/clojure.core/cond).

`and` and `or` allow you to combine conditions and `not` negates a condition, just like in Racket. The only difference is that instead of taking only boolean (true/false) expressions, Clojure allows any values to be combined using `and`, `or`, and `not`. The only values that are interpreted as false are `false` and `nil`. Everything else is considered true.
```clojure
(and (< 2 3) (<= 6 5)) ; results in false
(or (< 2 3) (<= 6 5)) ; results in true
(not (and (< 2 3) (<= 6 5))) ; results in true
(not (or (< 2 3) (<= 6 5))) ; results in false
```
See documentation for [and](https://clojuredocs.org/clojure.core/and), [or](https://clojuredocs.org/clojure.core/or), and [not](https://clojuredocs.org/clojure.core/not).


### nil
`nil` is a special value in Clojure. You can think of it as meaning "nothing" or "no answer". The convention is to return `nil` from functions that do not return any meaningful value, as you will see below for hashmaps and lists. `nil` is different from any other value in Clojure.

As you have seen above, `nil` is interpreted to be false in boolean expressions:
```clojure
(if nil 2 3) ; results in 3
```


### Hashmaps
Clojure doesn't use structures the way Racket does. Instead it uses hashmaps: collections of key/value pairs surrounded by curly braces. Hashmap are also referred to as just maps. 

For the purposes of this study we consider only hashmaps in which keys are a special Clojure datatype known as keywords. Keywords are any names preceded by a colon `:`. For instance, the following hashmap
```clojure
{:x 50, :y 100} ; hashmap in which :x has a value 50, and :y has a value 100
```
Note that commas are optional: the same hashmap can be written as `{:x 50 :y 100}`.

Hashmaps can be stored in variables:
```clojure
(def point1 {:x 50, :y 100} ) ; point1 now refers to the hashmap
```
Keywords can be used as selectors for hashmap fields. For instance, assuming that `point1` is defined as above, we can get its x and y values like this:
```clojure
(:x point1) ; results in 50
(:y point1) ; results in 100
```
If there is no value for a keyword in a hashmap, `nil` is returned:
```clojure
(:z point1) ; results in nil
```
Hashmaps are immutable.


### Lists and common list functions
There are a variety of different ways of producing list-like data sequences in Clojure, but the ones used in Racket work in Clojure as well. Note that Clojure prints back lists without the "list" constructor or a quote.
```clojure
(list 1 2 3) ; results in list (1 2 3)
'(1 2 3) ; also results in list (1 2 3)
```
Just like in Racket, it is possible to combine different types of elements in the same list:
```clojure
'(1 "two" 3.0001)
```
An empty list can be represented as `(list )` or `'()`.

Documentation on [list constructor](https://clojuredocs.org/clojure.core/list)

Just like in Racket, one can use `first` and `rest` on lists and check if a list is empty with `empty?`:
```clojure
(def  numbers '(3 5 4))
(def short-list '(7))

(first numbers) ; results in 3
(first short-list) ; results in 7
(rest numbers) ; results in (list 5 4)
(rest short-list) ; results in the list ()
(empty? numbers) ; results in false
(empty? short-list) ; results in false
(empty? (rest short-list)) ; results in true
```
However, unlike in Racket, calling `first` and `rest` on an empty list is not an error: `first` on an empty list returns `nil`, and `rest` on an empty list returns an empty list:
```clojure
(first '()) ; results in nil
(rest '()) ; results in the list ()
```

Just like in Racket, one can use `cons` to create a new list with an element added in the front of a given list:
```clojure
(def numbers '(3 5 4))
(cons 0 numbers) ; results in (0 3 5 4)
```
Documentation on [cons](https://clojuredocs.org/clojure.core/cons)


### Recursion on lists
Recursive functions in Clojure can be written exactly the same way as in Racket, with the exception of a slightly different syntax for specifying the function name and parameters. Below is the function that adds up all the numbers in a list of numbers:
```clojure
(defn add-all [numbers]
  (if (empty? numbers)
      0 ; base case
      (+ (first numbers) (add-all (rest numbers))))) ; recursive call

(add-all '(3 4 5 2)) ; results in 14

(add-all '()) ; results in 0
```
The next example shows a recursive function with two parameters that creates a list of the first n elements of a given list:
```clojure
(defn take-n [elements n]
  (if (or (empty? elements) (<= n 0))
    '()
    (cons (first elements) (take-n (rest elements) (- n 1)))))

(take-n '(2 5 6 7 1) 3) ; results in (list 2 5 6)
(take-n '(2 5 6 7 1) 10) ; results in (list 2 5 6 7 1)
(take-n '(2 5 6 7 1) 0) ; results in an empty list
```


### map, reduce, and similar functions on lists
Clojure has `map` and `filter` function that can be used exactly the same as the corresponding Racket functions:
```clojure
;; mapping inc (increment) function:
(map inc '(3 2 -1)) ; results in the list (4 3 0)
;; creating a list of string lengths:
(map count '("hi" "bye" "")) ; results in the list (2 3 0)

(filter odd? '(2 3 5 4 0 7)) ; results in (list 3 5 7)
(defn short? [s]
  (<= (count s) 5))

(filter short? '("apple" "avocado" "kiwi" "banana")) ; results in the list ("apple" "kiwi")
```
Documentation for [map](https://clojuredocs.org/clojure.core/map), [filter](https://clojuredocs.org/clojure.core/filter)

A Clojure function similar to Racket's `foldr` is called `reduce`. There are two versions of `reduce`: the one with three arguments that is pretty much the same as `foldr` (on symmetric functions, such as `+`; we are not considering non-symmetric functions such as `-`), and the one with two arguments that essentially uses the first element of the list as a base.

TO-DO: switched arguments of reduce.  

For consistency with Racket we are using the version of reduce with three arguments:
```clojure
(def numbers '(3 5 4))
(reduce + 0 numbers) ; results in 12

;; combining all strings in a list into one string
;; str plays a role of string-append
(reduce str "" '("Hi " "there," " " "how " "are " "you?")) ; results in "Hi there, how are you?"
```
Documentation for [reduce](https://clojuredocs.org/clojure.core/reduce)


### Anonymous functions
Just like in Racket, anonymous fucntions are often used as parameters for `map`, `reduce`, and other higher-order functions.
There are different ways of declaring anonymous functions in Clojure. Our examples use the `fn` keyword for this purpose.
The syntax is very similar to `defn`, except that instead of `defn` and the function name we use `fn`.

For instance, `(fn [x] (+ x 2))` is a function that takes one parameter `x` and returns `x` incremented by 2. If we map this function over a list, we create a new list in which every element is obtained from the given list by adding 2. Functions passed to `map` or to any other higher-order functions must be included in parentheses.
```clojure
(map (fn [x] (+ x 2))  '(2 3 1)) ;; results in the list (4 5 3)
```
Here `filter` uses an anonymous function `(fn [x] (>= x 5))` to select all elements of a list that are 5 or larger.
```clojure
(filter (fn [x] (>= x 5)) '(5 2 6 7 1 8)) ; results in the list (5 6 7 8)
```
Here `x` is the element of the list, and `y` is the result accumulated so far. For instance, in the example below `x` would be the currrent string, and `y` would be the sum of the length of strings encountered up to this point. Note that unlike `foldr` in Racket, `reduce` in Clojure traverses the list left-to-right (from the first element to the end).
```clojure
(reduce (fn [x y] (+ x (count y))) 0 '("hi" "bye" "hello")) ; results in 10
```
Documentation for [fn](https://clojuredocs.org/clojure.core/fn)
