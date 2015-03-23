Exercise 1.11
============

## Question

A function *f* is defined by the rule that *f(n) = n* if *n < 3* and *f(n) = f(n - 1) + 2f(n - 2) + 3f(n - 3)* if *n >= 3*. Write a procedure that computes *f* by means of a recursive process. Write a procedure that computes *f* by means of an iterative process.


## Answer

```scheme
;; recursive process
(define (f n)
  (cond ((< n 3) n)
        (else (+ (f (- n 1)) (f (- n 2)) (f (- n 3))))))

(f 5)
(+ (f 4) (f 3) (f 2))
(+ (+ (f 3) (f 2) (f 1)) (+ (f 2) (f 1) (f 0)) 2)
(+ (+ (+ (f 2) (f 1) (f 0)) 2 1) (+ 2 1 0) 2)
(+ (+ (+ 2 1 0) 2 1) 3 2)
(+ (+ 3 2 1) 3 2)
(+ 6 3 2)
11


;; iterative process
(define (f-iter x y z counter max)
  (if (= counter max)
      x
      (f-iter (+x y z) x y (+ counter 1) max))

(define (f n)
  (if (< n 3)
      n
      (f-iter 3 2 1 3 n)))
```


## Notes

No notes on this one. solutions page is down, but I verified my iterative process against the recursive process and I'm getting the same numbers so this should be good. May come back later once the site is up and add more notes. I'd like to add that I found the iterative process by running the recursive several times and realizing it's like fibonacci, but instead of adding the last 2 it adds the last 3.
