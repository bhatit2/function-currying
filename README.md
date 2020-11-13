# function-currying

In functional programming, currying is the process of converting a function, that takes multiple arguments at once, to a function that takes these arguments step by step.
Given a function with 3 parameters, the curried version will take one argument and return a function that takes the next argument, which returns a function that takes the third argument. The last function returns the result of applying the function to all of its arguments.

> Currying doesn’t call a function. It just transforms it.



## How does it work?
A function F that takes in arguments A, B, C and returns a value R, when curried, can be broken down into three functions X, Y, Z.

Function X takes in A as an argument and returns a function Y, which in turn takes in B as an argument and returns a function Z, which takes in C as an argument and finally returns the required value R.

## Example for 2 arguments function

Lets see a simple example. We’ll create a helper function curry(f) that performs currying for a two-argument f. In other words, curry(f) for two-argument f(a, b) translates it into a function that runs as f(a)(b)

```
function curry(f) { // curry(f) does the currying transform
  return function(a) {
    return function(b) {
      return f(a, b);
    };
  };
}

// usage
function sum(a, b) {
  return a + b;
}

let curriedSum = curry(sum);

alert( curriedSum(1)(2) ); // 3
```

## Advanced implementation

Here is an advanced implementation which will work for multi-argument functions 

```
function curry(func) {

  return function curried(...args) {
    if (args.length >= func.length) {
      return func.apply(this, args);
    } else {
      return function(...args2) {
        return curried.apply(this, args.concat(args2));
      }
    }
  };

}

function sum(a, b, c) {
  return a + b + c;
}

let curriedSum = curry(sum);

alert( curriedSum(1, 2, 3) ); // 6, still callable normally
alert( curriedSum(1)(2,3) ); // 6, currying of 1st arg
alert( curriedSum(1)(2)(3) ); // 6, full currying
```
