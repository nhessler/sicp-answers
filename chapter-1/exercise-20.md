Exercise 1.20
============

## Question

The process that a procedure generates is of course dependent on the rules used by the interpreter. As an example, consider the iterative ```gcd``` procedure given above. Suppose we were to interpret this procedure using normal-order evaluation, as discussed in section 1.1.5. (The normal-order-evaluation rule for if is described in exercise 1.5.) Using the substitution method (for normal order), illustrate the process generated in evaluating ```(gcd 206 40)``` and indicate the remainder operations that are actually performed. How many remainder operations are actually performed in the normal-order evaluation of ```(gcd 206 40)```? In the applicative-order evaluation?

```scheme
(define (gcd a b)
  (if (= b 0)
      a
      (gcd b (remainder a b))))
```


## Answer

**normal order**

```scheme
;; (remainder count 0)
(gcd 206 40)

;; substitute gcd for body of gcd (remainder count 0)
(if (= 40 0) 206 (gcd 40 (remainder 206 40)))

;; evaluate condition of if (remainder count 0)
(if false 206 (gcd 40 (remainder 206 40)))

;; evaluate if (remainder count 0)
(gcd 40 (remainder 206 40))

;; substitute gcd for body of gcd (remainder count 0)
(if (= (remainder 206 40) 0) 40 (gcd (remainder 206 40) (remainder 40 (remainder 206 40))))

;; evaluate condition of if (remainder count 1)
(if false 40 (gcd (remainder 206 40) (remainder 40 (remainder 206 40))))

;; evautate if (remainder count 1)
(gcd (remainder 206 40) (remainder 40 (remainder 206 40)))

;; substitute gcd for body of gcd (remainder count 1)
(if (= (remainder 40 (remainder 206 40)) 0) (remainder 206 40) (gcd (remainder 40 (remainder 206 40)) (remainder (remainder 206 40) (remainder 40 (remainder 206 40)))))

;; evaluate condition of if (remainder count 3)
(if false (remainder 206 40) (gcd (remainder 40 (remainder 206 40)) (remainder (remainder 206 40) (remainder 40 (remainder 206 40)))))

;; evalutate if (remainder count 3)
(gcd (remainder 40 (remainder 206 40)) (remainder (remainder 206 40) (remainder 40 (remainder 206 40))))

;; substitute gcd for body of gcd (remainder count 3)
(if (= (remainder (remainder 206 40) (remainder 40 (remainder 206 40))) 0) (remainder 40 (remainder 206 40))  (gcd (remainder (remainder 206 40) (remainder 40 (remainder 206 40))) (remainder (remainder 40 (remainder 206 40)) (remainder (remainder 206 40) (remainder 40 (remainder 206 40))))))

;; evaluate condition of if (remainder count 7)
(if false  (remainder 40 (remainder 206 40)) (gcd (remainder (remainder 206 40) (remainder 40 (remainder 206 40))) (remainder (remainder 40 (remainder 206 40)) (remainder (remainder 206 40) (remainder 40 (remainder 206 40))))))

;; evaluate if (remainder count 7)
(gcd (remainder (remainder 206 40) (remainder 40 (remainder 206 40))) (remainder (remainder 40 (remainder 206 40)) (remainder (remainder 206 40) (remainder 40 (remainder 206 40)))))

;; substitute gcd for body of gcd (remainder count 7)
(if (= (remainder (remainder 40 (remainder 206 40)) (remainder (remainder 206 40) (remainder 40 (remainder 206 40)))) 0) (remainder (remainder 206 40) (remainder 40 (remainder 206 40))) (gcd (remainder (remainder 40 (remainder 206 40)) (remainder (remainder 206 40) (remainder 40 (remainder 206 40)))) (remainder (remainder (remainder 206 40) (remainder 40 (remainder 206 40))) (remainder (remainder 40 (remainder 206 40)) (remainder (remainder 206 40) (remainder 40 (remainder 206 40)))))))

;; evaluate condition of if (remainder count 14)
(if true (remainder (remainder 206 40) (remainder 40 (remainder 206 40))) (gcd (remainder (remainder 40 (remainder 206 40)) (remainder (remainder 206 40) (remainder 40 (remainder 206 40)))) (remainder (remainder (remainder 206 40) (remainder 40 (remainder 206 40))) (remainder (remainder 40 (remainder 206 40)) (remainder (remainder 206 40) (remainder 40 (remainder 206 40)))))))

;; evaluate if (remainder count 14)
(remainder (remainder 206 40) (remainder 40 (remainder 206 40)))

;; result (remainder count 18)
2
```
**applicative order**

```scheme
;; (remainder count 0)
(gcd 206 40)

;; substitute gcd for body of gcd (remainder count 0)
(if (= 40 0) 206 (gcd 40 (remainder 206 40)))

;; evaluate condition of if (remainder count 0)
(if false 206 (gcd 40 (remainder 206 40)))

;; evaluate if (remainder count 0)
(gcd 40 (remainder 206 40))

;; evaluate arguments (remainder count 0)
(gcd 40 6)

;; substitute gcd for body of gcd (remainder count 1)
(if (= 6 0) 40 (gcd 6 (remainder 40 6)))

;; evaluate condition of if (remainder conut 1)
(if false 40 (gcd 6 (remainder 40 6)))

;; evaluate if (remainder count 1)
(gcd 6 (remainder 40 6))

;; evaluate arguments (remainder count 1)
(gcd 6 4)

;; substitute gcd for body of gcd (remainder count 2)
(if (= 4 0) 6 (gcd 4 (remainder 6 4)))

;; evaluate condition of if (remainder count 2)
(if false 6 (gcd 4 (remainder 6 4)))

;; evaluate if (remainder count 2)
(gcd 4 (remainder 6 4))

;; evaluate arguments (remainder count 2)
(gcd 4 2)

;; substitute gcd for body of gcd (remainder count 3)
(if (= 2 0) 4 (gcd 2 (remainder 4 2)))

;; evaluate condition of if (remainder count 3)
(if false 4 (gcd 2 (remainder 4 2)))

;; evaluate if (remainder count 3)
(gcd 2 (remainder 4 2))

;; evaluate arguments (remainder count 3)
(gcd 2 0)

;; substitute gcd for body of gcd (remainder count 4)
(if (= 0 0) 2 (gcd 0 (remainder 2 0)))

;; evaluate condition of if (remainder count 4)
(if true 2 (gcd 0 (remainder 2 0)))

;; evaluate if (remainder count 4)
2

;; result (remainder count 4)
2
```


## Notes

Solution is similar to my breakdown.
