# Strings

+ [Longest Substring Without Repeating Characters](#longest-substring-without-repeating-characters)
+ [Longest Repeating Character Replacement](#longest-repeating-character-replacement)
+ [Minimum Window Substring](#minimum-window-substring)
+ [Group Anagrams](#group-anagrams)
+ [Valid Parentheses](#valid-parenthese)
+ [Generate Parentheses](#generate-parentheses)
+ [Valid Palindrome](#valid-palindrome)
+ [Longest Palindromic Substring](#longest-palindromic-substring)
+ [Palindromic Substrings](#palindromic-substrings)
+ [Is Subsequence](#is-subsequence)

# Longest Substring Without Repeating Characters

https://leetcode.com/problems/longest-substring-without-repeating-characters/

```C++
class Solution {
 public:
  int lengthOfLongestSubstring(string s) {
    vector<char> letters;
    int result;
    int maxLength = 0;
    int length = 0;
    for (auto character : s) {
      auto founded = find(letters.begin(), letters.end(), character);
      if (founded != letters.end()) {
        maxLength = max(length, maxLength);
        length = letters.size() - (founded + 1 - letters.begin());
        letters.erase(letters.begin(), founded + 1);
      }
      length++;
      letters.push_back(character);
    }
    return max(maxLength, length);
  }
};
```

# Longest Repeating Character Replacement

https://leetcode.com/problems/longest-repeating-character-replacement/

```C++
class Solution {
 public:
  int characterReplacement(string s, int k) {
    int maxCount = 0;
    int left = 0;
    int count['Z' - 'A' + 1] = {0};
    int answer = 0;
    for (int right = 0; right < s.size(); right++) {
      int windowSize = right - left + 1;
      maxCount = max(maxCount, ++count[s[right] - 'A']);
      if (windowSize - maxCount > k) {
        count[s[left++] - 'A']--;
      } else {
        answer = max(answer, windowSize);
      }
    }
    return answer;
  }
};
```

# Minimum Window Substring

https://leetcode.com/problems/minimum-window-substring/

```C++
class Solution {
 public:
  string minWindow(string s, string t) {
    int tLetters[128] = {0};
    int curTLetters[128] = {0};
    for (auto letter : t) {
      tLetters[letter]++;
      curTLetters[letter]++;
    }
    int tLetNum = t.length();
    int left = 0;
    string answer;

    for (int right = 0; right < s.size(); right++) {
      if (!isInString(tLetters, s[right])) continue;
      if (!isEnoughString(curTLetters, s[right])) {
        tLetNum--;
      }
      curTLetters[s[right]]--;
      while (left <= right && tLetNum == 0) {
        if (!isInString(tLetters, s[left])) {
          left++;
          continue;
        }
        curTLetters[s[left]]++;
        if (!isEnoughString(curTLetters, s[left])) {
          tLetNum++;
          if (!answer.length() || right - left + 1 < answer.length())
            answer = s.substr(left, right - left + 1);
        }
        left++;
      }
    }
    return answer;
  }
  bool isInString(int tLetters[], char symbol) { return tLetters[symbol] != 0; }
  bool isEnoughString(int tLetters[], char symbol) {
    return tLetters[symbol] <= 0;
  }
};
```
# Group Anagrams

https://leetcode.com/problems/group-anagrams/

```C++
class Solution {
 public:
  vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> anagrams;
    for (auto word : strs) {
      string key = word;
      sort(key.begin(), key.end());
      if (anagrams.find(key) != anagrams.end()) {
        anagrams[key].push_back(word);
      } else {
        anagrams.insert(make_pair(key, vector<string>{word}));
      }
    }
    vector<vector<string>> answer;
    for (auto anagram : anagrams) {
      answer.push_back(anagram.second);
    }
    return answer;
  }
};
```

# Valid Parentheses

https://leetcode.com/problems/valid-parentheses/

```C++
class Solution {
 public:
  bool isValid(string s) {
    stack<char> brackets;
    for (auto character : s) {
      if (character == ')' || character == '}' || character == ']') {
        if (brackets.empty() || abs(brackets.top() - character) > 2) {
          return false;
        } else {
          brackets.pop();
        }
      } else {
        brackets.push(character);
      }
    }
    return brackets.empty();
  }
};
```

# Generate Parentheses

https://leetcode.com/problems/generate-parentheses/

```C++
class Solution {
 private:
  vector<string> answer;
  int amount;

 public:
  vector<string> generateParenthesis(int n) {
    amount = n;
    parenthesisVariants("", 0, 0);
    return answer;
  }
  void parenthesisVariants(string cur, int openNum, int closeNum) {
    if (cur.length() == 2 * amount) {
      answer.push_back(cur);
      return;
    }
    if (openNum < amount) parenthesisVariants(cur + "(", openNum + 1, closeNum);
    if (closeNum < openNum)
      parenthesisVariants(cur + ")", openNum, closeNum + 1);
  }
};
```

# Valid Palindrome

https://leetcode.com/problems/valid-palindrome/

```C++
class Solution {
 public:
  bool isPalindrome(string s) {
    int right = s.length() - 1;
    int left = 0;
    while (right >= left) {
      while (right >= left && !isalpha(s[right]) && !isdigit(s[right])) right--;
      while (right >= left && !isalpha(s[left]) && !isdigit(s[left])) left++;
      if (right >= left && tolower(s[left]) != tolower(s[right])) return false;
      right--;
      left++;
    }
    return true;
  }
};
```
# Longest Palindromic Substring

https://leetcode.com/problems/longest-palindromic-substring/

```C++
class Solution {
 public:
  string longestPalindrome(string s) {
    string answer;
    for (int mid = 0; mid < int(2 * s.length()); mid++) {
      int left = mid / 2;
      int right = left + mid % 2;
      while (left >= 0 && right < s.length() && s[left] == s[right]) {
        left--;
        right++;
      }
      right--;
      left++;
      if (right - left + 1 > answer.length()) {
        answer = s.substr(left, right - left + 1);
      }
    }
    return answer;
  }
};
```

# Palindromic Substrings

https://leetcode.com/problems/palindromic-substrings/

```C++
class Solution {
 public:
  int countSubstrings(string s) {
    int answer = 0;
    for (int mid = 0; mid < 2 * s.length() - 1; mid++) {
      int left = mid / 2;
      int right = left + mid % 2;
      while (left >= 0 && right < s.length() && s[left] == s[right]) {
        left--;
        right++;
        answer++;
      }
    }
    return answer;
  }
};
```

# Is Subsequence

https://leetcode.com/problems/is-subsequence/

```C++
class Solution {
 public:
  bool isSubsequence(string s, string t) {
    for (auto symbol : t) {
      if (s.empty()) break;
      if (symbol == s[0]) s.erase(0, 1);
    }
    return s.empty();
  }
};
```
