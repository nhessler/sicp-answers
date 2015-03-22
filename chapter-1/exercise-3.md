Exercise 1.3
============

## Question

Define a procedure that takes three numbers as arguments and returns the sum of the squares of the two larger numbers.


## Answer

```scheme
(define (square n n) (* n n))

(define (sum-of-squares x y) (+ (square x) (square y)))

(define (sum-squares-of-two-largest a b c)
    (cond ((= (min a b c) a) (sum-of-squares b c))
          ((= (min a b c) b) (sum-of-squares a c))
          (else (sum-of-squares b c))))

(sum-squares-of-two-largest 1 2 3) ;;=> 13
(sum-squares-of-two-largest 2 1 3) ;;=> 13
(sum-squares-of-two-largest 2 3 1) ;;=> 13
```


## Notes

I didn't try hard, but I was unable to define methods inside of methods using guile. The solutions page also has a wide variety of solutions that all look very cool
