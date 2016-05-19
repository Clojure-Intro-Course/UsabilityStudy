## Review of Racket

You will be using [Intermediate Student with lambda](https://docs.racket-lang.org/htdp-langs/intermediate-lam.html) level of Racket. Also make sure that in "Choose language" menu the Constant Style is set to "true false empty". 

Below is a very brief review of Racket elements used in this study, with examples and links to Racket documentation. 

### Infix notation
Racket follows infix notation, i.e. expressions are of the form `(function arg1 arg2...)`:
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

### Conditions and 'if'
The `if` statement is an expression that checks a if a condition is true, and one of the remaining two arguments, depending on whether the condition is true or false:
```racket
(define n 5)
(if (< n 10) 2 3) ; returns 2
(if (< n 2) 2 3)  ; returns 3
```
Our examples will not be using `cond` conditional, but here is a reminder on it in case you would like to use it:
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

### Common functions on numbers and strings
```racket

```

### Defining and using structures

### Lists, recursion on lists
<-- Note: we use if for recursion, not cond -->

### Common functions on lists

### Map, foldl, and other functions on lists

### Anonymous functions with lambda


