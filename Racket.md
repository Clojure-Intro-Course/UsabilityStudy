<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Racket](#racket)
	- [Review of Racket](#review-of-racket)
		- [How to run a Racket program](#how-to-run-a-racket-program)
		- [Prefix notation](#prefix-notation)
		- [Defining functions and variables](#defining-functions-and-variables)
		- [Common functions on numbers and strings](#common-functions-on-numbers-and-strings)
		- [Conditionals: 'if', 'cond', and combining conditions](#conditionals-if-cond-and-combining-conditions)
		- [Defining and using structures](#defining-and-using-structures)
		- [Lists](#lists)
		- [Common functions on lists](#common-functions-on-lists)
		- [Recursion on lists](#recursion-on-lists)
		- [map, foldr, and other functions on lists](#map-foldr-and-other-functions-on-lists)
		- [Anonymous functions with lambda](#anonymous-functions-with-lambda)

<!-- /TOC -->

# Racket

## Review of Racket

You will be using [Intermediate Student with lambda](https://docs.racket-lang.org/htdp-langs/intermediate-lam.html) level of Racket. Also make sure that in "Choose language" menu the Constant Style is set to "true false empty".

Below is a very brief review of Racket elements used in this study, with examples and links to Racket documentation.


### How to run a Racket program
Copy-paste the examples into the upper panel of the Racket window. You can run your program by pressing the Run button or Ctrl-R. The results and error messages will appear in the lower panel.

If your program starts and doesn't stop (the little figure in the right lower corner is running), press the red square at the top right to stop it.


### Prefix notation
Racket follows prefix notation, i.e. expressions are of the form `(function arg1 arg2...)`:
```racket
(+ 1 2 3 4) ; returns 10
(even? 2) ; returns true
(<= 4 3) ; returns false
```


### Defining functions and variables
```racket
; define a variable
(define n 5)

; define a function
(define (f x)
  (+ x 10))

; call a function
(f n)
```
Documentation for [define](https://docs.racket-lang.org/htdp-langs/intermediate-lam.html#%28form._%28%28lib._lang%2Fhtdp-intermediate-lambda..rkt%29._define%29%29)


### Common functions on numbers and strings
Coomon functions on numbers include the standard arithmetic operations and some predicates that allow us to check whether a number has a given property (for instance, whether it's even). There are functions `add1` and `sub1` that return the next or the previous integer for a given integer, see examples below. There are also many functions on strings, but our examples do not use them much. The `string-length` function below is a reminder of how string functions work in Racket.
```racket
;; common functions on numbers
(+ 2 3) ; results in 5
(* 2 3 4) ; results in 24
;; predicates (functions that return true/false) often end with ?
(even? 3) ; results in false
(odd? 3) ; results in true

;; add 1 and subtract 1 functions:
(add1 5) ; results in 6
(sub1 5) ; results in 4   

;; find out the length of a string:
(string-length "abc") ; results in 3
```
Documentation for [common numeric functions](https://docs.racket-lang.org/htdp-langs/beginner.html#%28part._htdp-beginner._.Numbers__.Integers__.Rationals__.Reals__.Complex__.Exacts__.Inexacts%29)


### Conditionals: 'if', 'cond', and combining conditions
The `if` statement is an expression that checks a if a condition is true, and one of the remaining two arguments, depending on whether the condition is true or false:
```racket
(define n 5)
(if (< n 10) 2 3) ; returns 2
(if (< n 2) 2 3)  ; returns 3
```
If you have more than two cases in a conditional, it's  convenient to use `cond` conditional:
```racket
(cond
  [(< n 5) "apple"]
  [(> n 5) "banana"]
  [else "orange"])
```
This expression returns the string "apple" if `n`is less than 5, "banana" if it's greater than 5, and "orange" if it's equal to 5.

Links for more details on [`if`](https://docs.racket-lang.org/htdp-langs/beginner.html#%28form._%28%28lib._lang%2Fhtdp-beginner..rkt%29._if%29%29) and [`cond`](https://docs.racket-lang.org/htdp-langs/beginner.html#%28form._%28%28lib._lang%2Fhtdp-beginner..rkt%29._cond%29%29).

You can combine conditions using `and` and `or` and negate them using `not`:
```racket
(define x 5)
(define y 6)

(if (and (<= x 5) (= y 5)) "hi" "bye")  ; returns "bye"
(if (or (<= x 5) (= y 5)) "hi" "bye") ; returns "hi"
(if (not (<= x 5)) "hi" "bye") ; returns "bye"
```
Links for more details on [`and` and `or`](https://docs.racket-lang.org/htdp-langs/beginner.html#%28form._%28%28lib._lang%2Fhtdp-beginner..rkt%29._and%29%29).


### Defining and using structures
Structures allow you to combine multiple data items into one entity with multiple fields. A structure datatype is defined by `define-struct`, and structure instances are created by `make-` followed by the structure name (known as a _constructor_):
```racket
;; define a structure type date with fields day, month, year
(define-struct date (day month year)) ;; (define-struct date [day month year]) also works
;; create two instances:
(define end-of-semester (make-date 6 "May" 2016))
(define 4th-of-July (make-date 4 "July" 2016))
```
Note that the structures are displayed with their constuctor. For instances, typing `end-of-semester` in the interpreter will result in `(make-date 6 "May" 2016)`

To access a specific field of a structure, you need to use a selector. A selector has the form of the structure name, followed by a dash `-`, followed by the field name:
```racket
(date-month end-of-semester) ; results in "May"
(date-day 4th-of-July) ; results in 4
```
Links for more details on [structures](https://docs.racket-lang.org/htdp-langs/beginner.html#%28form._%28%28lib._lang%2Fhtdp-beginner..rkt%29._define-struct%29%29) and the [textbook chapter on structures](http://www.ccs.neu.edu/home/matthias/HtDP2e/part_one.html#%28part._sec~3astructures%29)


### Lists
There are multiple ways of creating lists in Racket. We will be using the quote symbol `'` to create a list:
```racket
'(1 2 3) ; results in the list '(1 2 3), also displayed as (list 1 2 3)
```
It is possible to combine different types of elements in the same list:
```racket
'(1 "two" 3.0001)
```
A list with no elements is known as an empty list and can be created as`'()` or, equivalently, as `empty`.


### Common functions on lists
Common functions on lists include `first` (returns the first element of a list), `rest` (returns the rest of the list), and a predicate `empty?` that returns `true` if the list is empty and `false` otherwise:
```racket
(define numbers '(3 5 4))
(define short-list '(7))

(first numbers) ; results in 3
(first short-list) ; results in 7
(rest numbers) ; results in (list 5 4)
(rest short-list) ; results in empty
(empty? numbers) ; results in false
(empty? short-list) ; results in false
(empty? (rest short-list)) ; results in true
```
Applying `first` or `rest` to an empty list results in an error.

The function `cons` creates a new list by adding an element at the front of a given list:
```racket
(cons 0 '(3 5 4)) ; results in (list 0 3 4 5)
(cons 1 '()) ; results in (list 1)
```
The original list is unchanged.

See documentation for [cons](https://docs.racket-lang.org/htdp-langs/beginner.html#%28def._htdp-beginner._%28%28lib._lang%2Fhtdp-beginner..rkt%29._cons%29%29)


### Recursion on lists
Recursion on lists typically involves the base case of an empty list and a recursive case that
combines some operation on the first of the list with the result of a recursive call on the rest of the list.

The following function adds all elements of a list of numbers:
```racket
(define (add-all numbers)
  (if (empty? numbers)
      0 ; base case
      (+ (first numbers) (add-all (rest numbers))))) ; recursive call

(add-all '(3 4 5 2)) ; results in 14

(add-all '()) ; results in 0
```
There may be cases when a recursive function takes more than one parameter. The following function returns the first n elements of a list:
```racket
(define (take-n elements n)
  (if (or (empty? elements) (<= n 0))
      empty
      (cons (first elements) (take-n (rest elements) (- n 1)))))

(take-n '(2 5 6 7 1) 3) ; results in (list 2 5 6)
(take-n '(2 5 6 7 1) 10) ; results in (list 2 5 6 7 1)
(take-n '(2 5 6 7 1) 0) ; results in an empty list
```

<!--- TO-DO: need to be careful to avoid the study examples. --->


### map, foldr, and other functions on lists
Higher order functions on lists, such as `map, filter, foldr` provide a way of performing many types of common list operations without having to write recursive functions.

`map` takes a function and a list and returns a new list which is the result of applying the function to each element:
```racket
(map add1 '(3 2 -1)) ; results in (list 4 3 0)
(map string-length '("hi" "bye" "")) ; results in (list 2 3 0)
```
See documentation for [map](https://docs.racket-lang.org/htdp-langs/intermediate-lam.html#%28def._htdp-intermediate-lambda._%28%28lib._lang%2Fhtdp-intermediate-lambda..rkt%29._map%29%29)

`filter` takes a predicate (a function that returns true or false) and a list and creates a new list with only the elements of the given list that satisfy the predicate:
```racket
(filter odd? '(2 3 5 4 0 7)) ; results in (list 3 5 7)

(define (short? str)
  (<= (string-length str) 5))

(filter short? '("apple" "avocado" "kiwi" "banana")) ; results in (list "apple" "kiwi")
```
See documentation for [filter](https://docs.racket-lang.org/htdp-langs/intermediate-lam.html#%28def._htdp-intermediate-lambda._%28%28lib._lang%2Fhtdp-intermediate-lambda..rkt%29._filter%29%29)

`foldr` takes a function, a value to be returned from the base case, and a list, and returns the result of repeatedly applying the function to the current list element and the accumulated result. The simplest, and most common, example is adding all elements in a list of numbers:
```racket
(define numbers '(3 5 4))
(foldr + 0 numbers) ; results in 12
```
We can also use `foldr` to combine all strings in a list into one string:
```racket
(foldr string-append "" '("Hi " "there," " " "how " "are " "you?")) ; results in "Hi there, how are you?"
```
See documentation for [foldr](https://docs.racket-lang.org/htdp-langs/intermediate-lam.html#%28def._htdp-intermediate-lambda._%28%28lib._lang%2Fhtdp-intermediate-lambda..rkt%29._foldr%29%29)


### Anonymous functions with lambda
Calling higher-order functions, such as `map,filter`, etc., with simple, but not predefined, functions can be done by creating a function without a name (i.e. anonymous) on-the-fly using a `lambda` keyword.

The keyword `lambda` is followed by parameter(s) in parentheses, and then the body of the function. For instance,
`(lambda (x) (+ x 2))` is a function of one parameter `x` that returns the result of adding 2 to `x`. We can use this function in `map` to create a new list by adding 2 to every element of a given list:
```racket
(map (lambda (x) (+ x 2)) '(2 3 1)) ; results in (list 4 5 3)
```
We can also use anonymous functions in `filter` (the function must return true/false):
```racket
(filter (lambda (x) (>= x 5)) '(5 2 6 7 1 8)) ; results in (list 5 6 7 8)
```

In the case of `foldr` the anonymous function takes two parameters. The first one is list element, and the second one is the current accumulated result. For instance, the anonymous function below is used to compute the sum of the lengths of all strings in the given list. Here x will refer to each string of the list in turn, and y would respresent the sum of the lengths of all strings to the right of the string x:
```racket
(foldr (lambda (x y) (+ (string-length x) y)) 0 '("hi" "bye" "hello")) ; results in 10
```

More details on [lambda](http://www.ccs.neu.edu/home/matthias/HtDP2e/part_three.html#%28part._sec~3aint-lambda%29).
