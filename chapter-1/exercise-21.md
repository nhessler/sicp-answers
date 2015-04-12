Exercise 1.21
============

## Question

Use the ```smallest-divisor``` procedure to find the smallest divisor of each of the following numbers: 199, 1999, 19999.

```scheme
(define (smallest-divisor n)
  (find-divisor n 2))

(define (find-divisor n test-divisor)
  (cond ((> (square test-divisor) n) n)
        ((divides? test-divisor n) test-divisor)
        (else (find-divisor n (+ test-divisor 1)))))

(define (divides? a b)
  (= (remainder b a) 0))
```


## Answer

Not sure what to do here. I ended up entering the functions needed into the interpreter and just plugging in the numbers

```scheme
(smallest-divisor 199)   ;;=> 199
(smallest-divisor 1999)  ;;=> 1999
(smallest-divisor 19999) ;;=> 7
```


## Notes

Looking at the solutions page this seems to be what was requested. not sure what to take away from this other than the somewhat surprising result that 19999 is not prime
