Exercise 1.6
============

## Question

Alyssa P. Hacker doesn't see why if needs to be provided as a special form. ``Why can't I just define it as an ordinary procedure in terms of cond?'' she asks. Alyssa's friend Eva Lu Ator claims this can indeed be done, and she defines a new version of if:

```scheme
(define (new-if predicate then-clause else-clause)
  (cond (predicate then-clause)
        (else else-clause)))
```

Eva demonstrates the program for Alyssa:

```scheme
(new-if (= 2 3) 0 5)
5

(new-if (= 1 1) 0 5)
0
```

Delighted, Alyssa uses new-if to rewrite the square-root program:

```scheme
(define (sqrt-iter guess x)
  (new-if (good-enough? guess x)
          guess
          (sqrt-iter (improve guess x)
                     x)))
```
What happens when Alyssa attempts to use this to compute square roots? Explain.


## Answer

The problem lies with the applicative-order evaluation of ```new-if```. This does not happen with ```if``` as it is a special form. Basically, the ```else-clause``` clause of ```new-if``` will get evaluated whether it should or not resulting in much more computation than is necessary since the else clause of ```sqrt-iter```. I'm not positive, but this could lead to an infinite loop.


## Notes

According to the solutions page this should lead to an infinite loop given we keep evaluating the else clause before we get inside the ```new-if``` procedure.
