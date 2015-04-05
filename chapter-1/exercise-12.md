Exercise 1.12
============

## Question

The following pattern of numbers is called Pascal's triangle.

```
     1
    1 1
   1 2 1
  1 3 3 1
 1 4 6 4 1
```

The numbers at the edge of the triangle are all 1, and each number inside the triangle is the sum of the two numbers above it. Write a procedure that computes elements of Pascal's triangle by means of a recursive process.


## Answer

```scheme
(define (pt-element row col)
  (cond ((or (< row col) (< col 1) (< row 1)) 0) ;; outside the triangle return 0
        ((or (= row col) (= col 1)) 1)           ;; edge of the triangle return 1
        (else (+ (pt-element (- row 1) (- col 1)) (pt-element (- row 1) col)))))
```


## Notes

Had to read the method name and args of some of the results to realize what we were supposed to calculate. But once I got that it didn't take long to figure out the rest.
