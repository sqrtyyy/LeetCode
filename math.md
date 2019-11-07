# Mathematics
+ [Fibonacci Number](#fibonacci-number)
  + [Recursive](#recursive)
  + [Recursive with memorization](#recursive-with-memorization)
  + [Iterative](#iterative)
+ [Count Primes](#count-primes)

## Fibonacci Number

Here're different methods of calculating N's member of Fibonacci sequence.

https://leetcode.com/problems/fibonacci-number/

### Recursive

```C++
class Solution {
 public:
  int fib(int N) {
    if (N < 2) return N;
    return fib(N - 1) + fib(N - 2);
  }
};
```
### Recursive with memorization

```C++
class Solution {
 public:
  int fib(int N) {
    if (N < 2) return N;
    int memo[N + 1] = {0, 1};
    return FibRecursive(N, memo);
  }
  int FibRecursive(int N, int* memo) {
    if (N < 2) return N;
    if (!memo[N])
      memo[N] = FibRecursive(N - 1, memo) + FibRecursive(N - 2, memo);
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
    while (N) {
      int next = first + second;
      first = second;
      second = next;
      N--;
    }
    return first;
  }
};
```
## Count Primes

https://leetcode.com/problems/count-primes/

```C++
class Solution {
 public:
  int countPrimes(int n) {
    if (n == 0) return 0;
    bool A[n] = {false};
    for (int i = 2; i * i < n; i++) {
      if (!A[i]) {
        for (int j = i * i; j < n; j += i) A[j] = true;
      }
    }
    int answer = 0;
    for (int i = 2; i < n; i++)
      if (!A[i]) answer++;
    return answer;
  }
};
```
