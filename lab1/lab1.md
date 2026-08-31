# CSCI 3212 Lab 1

## Fibonacci numbers

Source: https://en.wikipedia.org/wiki/Fibonacci_sequence  

The Fibonacci sequence is a sequence of numbers where:  
1. The first and second numbers are both ``1``, that is, ``fibonacci(1) = fibonacci(2) = 1``
2. The numbers that follow are the sum of the previous TWO numbers, so  
``fibonacci(3) = fibonacci(2) + fibonacci(1) = 1 + 1 = 2``  
``fibonacci(4) = fibonacci(3) + fibonacci(2) = 2 + 1 = 3``.

```
TODO: Answer the following questions:
fibonacci(5) = 5
fibonacci(6) = 8
fibonacci(7) = 13
fibonacci(8) = 21
fibonacci(9) = 34
```

## Basic implementation

Let's take a look at an implementation:
```python
def fibonacci(n):
    if n <= 0:
        return 0
    if n == 1:
        return 1
    return fibonacci(n-1) + fibonacci(n-2)
```
You can also find this in ``algorithms-labs-gw26/lab1/fibonacci.py``, and run it: 
```bash
cd algorithms-labs-gw26/lab1
python fibonacci.py
```
The code version also tells you how much time does it take to complete each calculation.
```
TODO:
1. Explain what the code above is doing.
A: The code takes a number n, and computes the sum of the previous 2 numbers in the fibonacci sequence to get the nth number of the fibonacci sequence.
2. What happens if we remove the "if ... return ..." and only keep the last line?
A: The program will run until a StackOverflow error occurs, because there would be no base case.
3. What is fibonacci(20)? how much time did it take to calculate that?
A: 6765, it took 9.0340e-04 seconds to calculate.
4. What is fibonacci(30)? how much time did it take to calculate that?
A: 832040, it took 7.8422e-02 seconds to calculate.
5. How much time did it take you to calculate fibonacci(40)? (this might take a while...)
A: 102334155, it took 8.8091e+00 seconds to calculate.
```

## How many function calls?

Modify ``fibonacci_counting.py`` so that it does the same calculation as ``fibonacci.py``, but it also counts how many times the function ``fibonacci(n)`` had to be called. Then answer the following:
```
TODO:
1. How many function calls does fibonacci(1) take?
A: 1 funccall.
2. How many function calls does fibonacci(5) take?
A: 15 funccalls.
3. How many function calls does fibonacci(10) take?
A: 177 funccalls.
4. Why is it so slow? Where does the complexity come from?
A: It's slow because each time the function is called, it calls 2 more copies of the function (with a slightly lower input), which do the same until the base case.
5. Is this O(n)? is this O(2^n)? Why?
A: This is not O(n) because it scales faster than linear. It is O(2^n) because every increase of 1 in the input size increases the number of function calls by ~double.
6. Is this Ω(n)? Why?
A: This is Ω(n) because for all n>=1, the number of function calls to compute fibonacci(n+1) increases by more than 1*a constant.
```

## Memoization Optimization

Take a look at ``fibonacci_memoized.py``, where memoization is used.
```
TODO:
1. How is this one different from the previous one?
A: This one logs all previous used fibonacci computations in a cache, so that after it is used once in the tree of fib calls, it does not need to be computed again.
2. How much time does it take to calculate fibonacci(30)?
A: 3.3002e-05 seconds.
3. Why is it often faster?
A: Eg this is in python on a mid-range laptop. If background tasks (like the GC) happened in this example, other run-throughs would potentially take much less time (I did it a few times and got runs between 1.2e-05 and 4.5e-05 seconds).
4. Also modify this file to count: how many times the function had to be called for fibonacci(30)?
A: 59 times.
5. Is this O(n)? is this O(2^n)? Why?
A: This is O(n) (and by default also O(2^n), though that description isn't very helpful), because each function call for fibonacci(n+1) only increases the total # of calls by ~2 calls (linear increase).
6. Is this Ω(n)? is this Ω(2^n)? Why?
A: This is Ω(n) because a function call fibonacci(n+1) for all n>1 increases the # of function calls by >=2 (a linear increase). It is not Ω(2^n) because that is faster growth than the function.
This function can be modelled as f=2n-1, where f is the total number of function calls for an input n.
```

## Extension: Staircase Problem

Implement ``fibonacci_threeway.py``, where:
1. The first, second, and third numbers are ``1``.
2. The numbers afterwards are the sum of the previous **THREE** numbers, instead of two.
3. Your implementation should be optimized, taking less than 1 second to calculate ``fibonacci_threeway(50)``.
A: Memoized, got fibonacci_threeway(50) = 4045078385041, calculating this took 1.1058e-04 seconds.

## Optional, challenge problems
1. Instead of recursion, implement ``fibonacci(n)`` using iteration instead.
A: see ``fibonacci.py`` (original solution commented out). 
2. ``fibonacci_memoized.py`` fails if you give it a very large input number such as one million - why? Try fixing it.
A: It fails due to recursion depth being exceeded. Did not try, ran out of time. 
3. There is an even faster way to calculate fibonacci numbers, in (almost) O(1) time. Read Wikipedia and try to implement it, or if you like a big challenge, implement it without looking it up.
A: ran out of time.