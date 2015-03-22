Exercise 1.8
============

## Question

Newton's method for cube roots is based on the fact that if y is an approximation to the cube root of x, then a better approximation is given by the value

((x / y^2) + 2y)/3

Use this formula to implement a cube-root procedure analogous to the square-root procedure. (In section 1.3.4 we will see how to implement Newton's method in general as an abstraction of these square-root and cube-root procedures.)


## Answer

```scheme
(define (improve guess x)
  (/ (+ (/ x (square guess)) (* 2 guess)) 3))

(define (square n) (* n n))

(define (cube n) (* n n n))

(define (good-enough? guess x)
  (< (abs (- (improve guess x) guess)) (* guess 0.001)))

(define (cube-root-iter guess x)
  (if (good-enough? guess x)
      guess
      (cube-root-iter (improve guess x) x)))

(define (cube-root x) (cube-root-iter 1.0 x))
```


## Notes

Checked in REPL and checked against solutions page. Found very similar examples. yay! feeling good about this. Although what I did was a bit of cut and paste from the square root solution and making it work for cube roots. That said, I understood the code enough to make the changes and basically got it right on the first try.
