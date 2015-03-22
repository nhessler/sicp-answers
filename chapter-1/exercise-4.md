Exercise 1.4
============

## Question

Observe that our model of evaluation allows for combinations whose operators are compound expressions. Use this observation to describe the behavior of the following procedure:

```scheme
(define (a-plus-abs-b a b)
  ((if (> b 0) + -) a b))
```


## Answer

If ```b``` is positive add it to ```a``` else subtract it from ```a```


## Notes

I think I did a good job of explaining the method, but I didn't describe what the ```if``` was returning. This is from the solutions page:

The ```if``` statement returns either a ```-``` or a ```+```, which is then applied to the operands.
