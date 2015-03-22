Exercise 1.5
============

## Question

Ben Bitdiddle has invented a test to determine whether the interpreter he is faced with is using applicative-order evaluation or normal-order evaluation. He defines the following two procedures:

```scheme
(define (p) (p))

(define (test x y)
  (if (= x 0)
      0
      y))
```

Then he evaluates the expression

```scheme
(test 0 (p))
```

What behavior will Ben observe with an interpreter that uses applicative-order evaluation? What behavior will he observe with an interpreter that uses normal-order evaluation? Explain your answer. (Assume that the evaluation rule for the special form if is the same whether the interpreter is using normal or applicative order: The predicate expression is evaluated first, and the result determines whether to evaluate the consequent or the alternative expression.)


## Answer

The definition of ```p``` is an infinite loop since all it does is call itself. defining this is fine, but we don't want it to be evaluated as it will never kick out. For applicative-order evaluation we'll get stuck in the infinite loop since the arguments are evaluated before they are passed to to ```test```. In normal-order evaluation we should get back ```0```. This is first due to the normal-order evaluation passing along the parameters ```0``` and ```(p)``` to the ```if``` replacing the ```x``` and ```y``` respectively without evaluating them. Next, the ```if``` will evaluate the predicate statement which returns ```#t``` and only evaluates the first expression returning ```0```.


## Notes

The solutions page had a much more concise answer, but I wanted to make sure I was clear. showing the substitution and evaluation steps would have been useful as was done in the solutions page.
