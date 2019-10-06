# Mathematics
+ [Fibonacci Number](#fib)
  + [Recursive](#fib_rec)
  + [Recursive with memorization](#fib_rec_memo)
  + [Iterative](#fib_iter)

## Fibonacci Number

Here's different methods of calculating N's member of Fibonacci sequence.

https://leetcode.com/problems/fibonacci-number/

### Recursive

```C++
class Solution {
public:
    int fib(int N) {
        if(N < 2)
            return N;
        return fib(N - 1) + fib(N - 2); 
    }
};
```
### Recursive with memorization

```C++
class Solution {
public:
    int fib(int N) {
        if(N < 2)
            return N;
        int memo[N + 1] = {0, 1};
        return FibRecursive(N, memo);        
    }
    int FibRecursive(int N, int* memo){
        if(N < 2)
            return N;
        if(!memo[N])
            memo[N]= FibRecursive(N - 1, memo) + FibRecursive(N - 2, memo);
        return memo[N];
    }
};
```
### Iterative

```C++
class Solution {
public:
    int fib(int N) {
        int first = 0;
        int second = 1;
        while(N){
            int next = first + second;
            first = second;
            second = next;
            N--;
        }
        return first;
    }
};
```
