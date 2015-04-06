Exercise 1.18
============

## Question

Using the results of exercises 1.16 and 1.17, devise a procedure that generates an iterative process for multiplying two integers in terms of adding, doubling, and halving and uses a logarithmic number of steps.


## Answer

*Copied from 1.17 where I already did this*

```scheme
(define (double n) (+ n n))

(define (halve n) (/ n 2))

(define (m-iter a b c)
  (cond ((= b 0) 0)
        ((= b 1) (+ a c)
        ((even? b) (m-iter (double a) (halve b) c))
        (else (m-iter a (- b 1) (+ a c))))))

(define (m a b)
  (m-iter a b 0))

;; test runs
(m 0 0)   ;;=> 0
(m 0 1)   ;;=> 0
(m 0 2)   ;;=> 0
(m 1 3)   ;;=> 3
(m 2 2)   ;;=> 4
(m 9 9)   ;;=> 81
(m 12 12) ;;=> 144
(m 6 4)   ;;=> 24
(m 6 5)   ;;=> 30
(m 13 13) ;;=> 169
```


## Notes

This could be a bit more concise with only 1 root case of b = 0 instead of b = 0 and b = 1
