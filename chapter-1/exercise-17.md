Exercise 1.17
============

## Question

The exponentiation algorithms in this section are based on performing exponentiation by means of repeated multiplication. In a similar way, one can perform integer multiplication by means of repeated addition. The following multiplication procedure (in which it is assumed that our language can only add, not multiply) is analogous to the expt procedure:

```scheme
(define (* a b)
  (if (= b 0)
      0
      (+ a (* a (- b 1)))))
```

This algorithm takes a number of steps that is linear in b. Now suppose we include, together with addition, operations double, which doubles an integer, and halve, which divides an (even) integer by 2. Using these, design a multiplication procedure analogous to fast-expt that uses a logarithmic number of steps.


## Answer

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

My answer is a bit better than the solutions in that it is iterative.
