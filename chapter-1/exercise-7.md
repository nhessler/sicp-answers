Exercise 1.7
============

## Question

```scheme
(define (average x y)
  (/ (+ x y) 2))

(define (improve guess x)
  (average guess (/ x guess)))

(define (square n) (* n n))

(define (good-enough? guess x)
  (< (abs (- (square guess) x)) 0.001))

(define (sqrt-iter guess x)
  (if (good-enough? guess x)
      guess
      (sqrt-iter (improve guess x)
                 x)))

(define (sqrt x) (sqrt-iter 1.0 x))

```


The ```good-enough?``` test used in computing square roots will not be very effective for finding the square roots of very small numbers. Also, in real computers, arithmetic operations are almost always performed with limited precision. This makes our test inadequate for very large numbers. Explain these statements, with examples showing how the test fails for small and large numbers. An alternative strategy for implementing ```good-enough?``` is to watch how ```guess``` changes from one iteration to the next and to stop when the change is a very small fraction of ```guess```. Design a ```square-root``` procedure that uses this kind of end test. Does this work better for small and large numbers?


## Answer

For small numbers we don't have enough of a delta between guesses to dig into the actual square root. you can see this with these 2 checks which end up with very similar square roots even though they are radically different. and squaring the final guess does not lead to a number similar to either of the last two numbers.

```scheme
(sqrt 0.00001)
0.03135649010771716

(sqrt 0.00000001)
0.03125010656242753

(sqrt 0.000000000001)
0.031250000010656254

(square 0.031250000010656254)
9.765625006660159e-4
```

For large numbers our delta requirement is too narrow and we could end up in an infinite loop which happened when trying to compute the sqare root of 123456789123456789123456789123456789.

```scheme
(sqrt 123456789123456789123456789123456789)
;; never got to a final answer. had to quit the process
```


The recommended change to ```good-enough?``` and functions that use it.

```scheme
;; original take on good-enough?
;; (define (good-enough? new-guess old-guess)
;;   (< (abs (- new_guess old_guess) 0.001)))

;; modified based on solutions page
(define (good-enough? new-guess old-guess)
  (< (abs (- new_guess old_guess)) (* old-guess 0.001)))

(define (sqrt-iter guess x)
  (if (good-enough (improve guess x) guess)
      guess
      (sqrt-iter (improve guess x) x)))
```

For small numbers this works out much better as it allows us to get at a square root based on a percentage of the original number. For large numbers this ends up not having enough fidelity and can lead to sqrts that are not really exact at all.

## Notes

My ```good-enough?``` method is not checking relative to the last guess. based on reading through the solutions page I should have done it this way. Making it a comparison of the percentage change instead of absolute change.

```scheme
(define (good-enough? new-guess old-guess)
  (< (abs (- new_guess old_guess)) (* old-guess 0.001)))
```
