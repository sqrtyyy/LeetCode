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

# Longest Repeating Character Replacement

https://leetcode.com/problems/longest-repeating-character-replacement/

# Minimum Window Substring

https://leetcode.com/problems/minimum-window-substring/

# Group Anagrams

https://leetcode.com/problems/group-anagrams/

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

# Palindromic Substrings

https://leetcode.com/problems/palindromic-substrings/

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
