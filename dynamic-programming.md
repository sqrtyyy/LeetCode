# Dynamic Programming

+ [Backpack](#backpack)
+ [Climbing Stairs](#climbing-stairs)
+ [Coin Change](#coin-change)
+ [Longest Increasing Subsequence](#longest-increasing-subsequence)
+ [Longest Common Subsequence](#longest-common-subsequence)
+ [Word Break](#word-break)
+ [Unique Paths](#unique-path)
+ [Unique Paths II](#unique-paths-ii)
+ [Jump Game](#jump-game)
+ [Jump Game II](#jump-game-ii)
+ [House Robber](#house-robber)
+ [House Robber II](#house-robber-ii)
+ [Decode Ways](#decode-ways)
+ [Coin Change 2](#coin-change-2)
+ [N-Queens](#n-queens)
+ [N-Queens II](#n-queens-ii)

## Backpack

https://stepik.org/lesson/13259/step/5?unit=3444

## Climbing Stairs

https://leetcode.com/problems/climbing-stairs/

```C++
class Solution {
 public:
  int climbStairs(int n) {
    int first = 0;
    int second = 1;
    while (n > 0) {
      second = first + second;
      first = second - first;
      n--;
    }
    return second;
  }
};
```

## Coin Change

https://leetcode.com/problems/coin-change/

## Longest Increasing Subsequence

https://leetcode.com/problems/longest-increasing-subsequence/

```C++
class Solution {
 public:
  int lengthOfLIS(vector<int>& nums) {
    vector<int> maxISArray(nums.size(), 0);
    int answer = 0;
    for (int i = 0; i < nums.size(); i++) {
      int maxIS = 1;
      for (int j = 0; j < i; j++)
        if (nums[i] > nums[j]) maxIS = max(maxIS, maxISArray[j]);
      maxISArray[i] = maxIS + 1;
      answer = max(answer, maxIS);
    }
    return answer;
  }
};
```

## Longest Common Subsequence

https://leetcode.com/problems/longest-common-subsequence/

## Word Break

https://leetcode.com/problems/word-break/

```C++
class Solution {
 public:
  bool wordBreak(string s, vector<string>& wordDict) {
    unordered_set<string> wordSet(wordDict.begin(), wordDict.end());
    unordered_map<string, bool> memo;
    return wordBreakHelp(s, wordSet, memo);
  }
  bool wordBreakHelp(string& s, unordered_set<string>& wordSet,
                     unordered_map<string, bool>& memo) {
    if (memo.find(s) != memo.end()) return memo[s];
    if (wordSet.find(s) != wordSet.end()) return memo[s] = true;
    for (int i = 1; i < s.size(); i++) {
      string rightPart = s.substr(i);
      if (wordSet.find(rightPart) == wordSet.end()) continue;
      string leftPart = s.substr(0, i);
      if (wordBreakHelp(leftPart, wordSet, memo)) return memo[s] = true;
    }
    return memo[s] = false;
  }
};
```
### Word Break II

https://leetcode.com/problems/word-break-ii/

```C++
class Solution {
 public:
  bool do_word_break(string& str, int position, vector<string>& wordDict,
                     vector<int>& results, vector<vector<string>>& resultVect) {
    if (results[position] != -1) return results[position];
    if (position == str.size()) return results[position] = true;
    bool isResult = false;
    for (auto word : wordDict) {
      if (!str.compare(position, word.size(), word))
        if (do_word_break(str, position + word.size(), wordDict, results,
                          resultVect)) {
          vector<string> newResult = resultVect[position + word.size()];
          if (newResult.size() == 0) resultVect[position].push_back(word);
          for (auto newWord : newResult)
            resultVect[position].push_back(word + " " + newWord);
          isResult = true;
        }
    }
    return results[position] = isResult;
  }

  vector<string> wordBreak(string s, vector<string>& wordDict) {
    vector<int> results(s.size() + 1, -1);
    vector<vector<string>> resultVect(s.size() + 1);
    do_word_break(s, 0, wordDict, results, resultVect);
    return resultVect[0];
  }
};
```
## Unique Paths

https://leetcode.com/problems/unique-paths/

```C++
class Solution {
 public:
  int uniquePaths(int m, int n) {
    vector<int> line(m, 0);
    vector<vector<int>> map(n, line);
    map[0][0] = 1;
    for (int i = 0; i < m; i++)
      for (int j = 0; j < n; j++) {
        if (j - 1 >= 0) map[j][i] += map[j - 1][i];
        if (i - 1 >= 0) map[j][i] += map[j][i - 1];
      }
    return map[n - 1][m - 1];
  }
};
```

## Unique Paths II

https://leetcode.com/problems/unique-paths-ii/

```C++
class Solution {
 public:
  int uniquePathsWithObstacles(vector<vector<int>>& map1) {
    if (map1[0][0] == 1) return 0;
    unsigned int map[map1.size()][map1[0].size()] = {};
    map[0][0] = 1;
    for (int i = 0; i < map1.size(); i++)
      for (int j = 0; j < map1[0].size(); j++) {
        if (map1[i][j] == 1) {
          if (i != 0 || j != 0) map[i][j] = 0;
          continue;
        }
        if (i - 1 >= 0) map[i][j] += map[i - 1][j];
        if (j - 1 >= 0) map[i][j] += map[i][j - 1];
      }
    return map[map1.size() - 1][map1[0].size() - 1];
  }
};
```
## Jump Game

https://leetcode.com/problems/jump-game/

```C++
class Solution {
 public:
  bool canJump(vector<int>& nums) {
    int last = nums.size() - 1;
    for (int i = nums.size() - 1; i >= 0; i--)
      if (i + nums[i] >= last) last = i;
    return last == 0;
  }
};
```

## Jump Game II

https://leetcode.com/problems/jump-game-ii/

## House Robber

https://leetcode.com/problems/house-robber/submissions/

```C++
class Solution {
 public:
  int rob(vector<int>& nums) {
    int prev = 0;
    int prev_prev = 0;
    for (auto num : nums) {
      int tmp = prev_prev;
      prev_prev = prev;
      prev = max(tmp + num, prev);
    }
    return prev;
  }
};
```

## House Robber II

https://leetcode.com/problems/house-robber-ii/

```C++
class Solution {
 public:
  int rob(vector<int>& nums) {
    if (nums.size() == 1) return nums[0];
    return max(rob(nums, nums.size() - 1, 0), rob(nums, nums.size(), 1));
  }
  int rob(vector<int>& nums, int end, int begin) {
    int prev = 0;
    int prev_prev = 0;
    for (int i = begin; i < end; i++) {
      int tmp = prev_prev;
      prev_prev = prev;
      prev = max(tmp + nums[i], prev);
    }
    return prev;
  }
};
```

## Decode Ways

https://leetcode.com/problems/decode-ways/

## Coin Change 2

https://leetcode.com/problems/decode-ways/

## N-Queens

https://leetcode.com/problems/n-queens/

## N-Queens II

https://leetcode.com/problems/n-queens-ii/
