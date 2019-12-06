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

```C++
int MaxWeight(int capacity, vector<int>& nums) {
  vector<vector<int>> maxValue(nums.size() + 1, vector<int>(capacity + 1));
  for (int i = 1; i <= nums.size(); i++) {
    for (int j = 1; j <= capacity; j++) {
      if (nums[i - 1] > j)
        maxWeight[i][j] = maxWeight[i - 1][j];
      else
        maxWeight[i][j] = max(maxWeight[i - 1][j],
                              maxWeight[i - 1][j - nums[i - 1]] + nums[i - 1]);
    }
  }
  return maxValue.back().back();
}
```

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

```C++
class Solution {
 public:
  int coinChange(vector<int>& coins, int amount) {
    vector<int> sums(amount + 1, amount + 1);
    sums[0] = 0;
    for (int i = 1; i <= amount; i++)
      for (auto coin : coins)
        if (coin <= i) sums[i] = min(sums[i], sums[i - coin] + 1);
    return sums.back() > amount ? -1 : sums.back();
  }
};
```

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

```C++
class Solution {
 public:
  int longestCommonSubsequence(string text1, string text2) {
    vector<vector<int>> sames(text1.length() + 1,
                              vector<int>(text2.length() + 1));
    for (int i = 1; i <= text1.length(); i++)
      for (int j = 1; j <= text2.length(); j++) {
        if (text1[i - 1] == text2[j - 1])
          sames[i][j] = 1 + sames[i - 1][j - 1];
        else
          sames[i][j] = max(sames[i][j - 1], sames[i - 1][j]);
      }
    return sames.back().back();
  }
};
```

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

```C++
class Solution {
 public:
  int jump(vector<int>& nums) {
    int jumpNum = 0, lastReach = 0;
    int reach = 0;
    for (int i = 0; i < nums.size() - 1; i++) {
      if (lastReach >= nums.size() - 1) break;
      reach = max(reach, i + nums[i]);
      if (i == lastReach) {
        jumpNum++;
        lastReach = reach;
      }
    }
    return jumpNum;
  }
};
```

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

```C++
class Solution {
 public:
  int numDecodings(string s) {
    int prev = 0, cur = 1;
    for (int i = 0; i < s.length(); i++) {
      if (s[i] == '0') cur = 0;
      int tmp = cur + prev;
      if (!cur && !prev) return 0;
      if (s[i] == '1' || s[i] == '2' && s[i + 1] <= '6')
        prev = cur;
      else
        prev = 0;
      cur = tmp;
    }
    return cur;
  }
};
```

## Coin Change 2

https://leetcode.com/problems/coin-change-2/

```C++
class Solution {
 public:
  int change(int amount, vector<int>& coins) {
    vector<int> num(amount + 1);
    num[0] = 1;
    for (int i = 0; i < coins.size(); i++)
      for (int j = coins[i]; j <= amount; j++) num[j] += num[j - coins[i]];
    return num.back();
  }
};
```

## N-Queens

https://leetcode.com/problems/n-queens/
```C++
class Solution {
 private:
  int size;
  vector<bool> LDiag;
  vector<bool> RDiag;
  vector<bool> usedLine;
  vector<vector<string>> results;
  vector<string> result;

 public:
  void putQueen(int column) {
    if (column == size) {
      results.push_back(result);
      return;
    }
    for (int line = 0; line < size; line++) {
      if (!usedLine[line] && !RDiag[line + column] &&
          !LDiag[column - line + size - 1]) {
        result[line][column] = 'Q';
        usedLine[line] = true;
        RDiag[line + column] = true;
        LDiag[column - line + size - 1] = true;
        putQueen(column + 1);
        result[line][column] = '.';
        usedLine[line] = false;
        RDiag[line + column] = false;
        LDiag[column - line + size - 1] = false;
      }
    }
  }
  vector<vector<string>> solveNQueens(int n) {
    result.resize(n, string(n, '.'));
    LDiag.resize(2 * n - 1, false);
    RDiag.resize(2 * n - 1, false);
    usedLine.resize(n, false);
    size = n;
    putQueen(0);
    return results;
  }
};
```

## N-Queens II

https://leetcode.com/problems/n-queens-ii/

```C++
class Solution {
 private:
  int size;
  int answer;
  vector<bool> LDiag;
  vector<bool> RDiag;
  vector<bool> usedLine;
  vector<string> result;

 public:
  void putQueen(int column) {
    if (column == size) {
      answer++;
      return;
    }
    for (int line = 0; line < size; line++) {
      if (!usedLine[line] && !RDiag[line + column] &&
          !LDiag[column - line + size - 1]) {
        result[line][column] = 'Q';
        usedLine[line] = true;
        RDiag[line + column] = true;
        LDiag[column - line + size - 1] = true;
        putQueen(column + 1);
        result[line][column] = '.';
        usedLine[line] = false;
        RDiag[line + column] = false;
        LDiag[column - line + size - 1] = false;
      }
    }
  }
  int totalNQueens(int n) {
    result.resize(n, string(n, '.'));
    LDiag.resize(2 * n - 1, false);
    RDiag.resize(2 * n - 1, false);
    usedLine.resize(n, false);
    size = n;
    putQueen(0);
    return answer;
  }
};
```
