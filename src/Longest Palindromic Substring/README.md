# Longest Palindromic Substring

## Question:

Given a string `s`, return the longest palindromic substring in `s`.

## How to Solve:

The idea is to iterate through the string `s`, and try to use each
character as the middle point of a palindrome. In other words, we
"expand" from each character and see how wide we could go. We keep
track of the longest palindromic substring and indices in the process.

One thing to watch out is that palindrome could be of odd length or
even length. That's why when we determine the middle point, we try
`expandPalindromeLength(s, n, i, i)` for odd-length palindrome cases,
and `expandPalindromeLength(s, n, i, i+1)` for even-length palindrome
cases, where `expandPalindromeLength()` returns the longest possible
palindrome using the index `i` as the middle point. At each iteration
we choose the longer of the two.

## My C++ Solution:

```cpp
class Solution {
 public:
  string longestPalindrome(string s) {
    int n = (int)s.length();
    int start = 0;    // starting index of current max palindrom
    int max_len = 0;  // max palindrome length seen so far
    for (int i = 0; i < n; ++i) {
      int cur = max(expandPalindromeLength(s, n, i, i),       // case odd
                    expandPalindromeLength(s, n, i, i + 1));  // case even
      if (cur > max_len)                                      // update both 'starting index' and 'max_len'
      {
        start = i - ((cur - 1) / 2);  // works for both odd and even len
        max_len = cur;
      }
    }
    return s.substr(start, max_len);
  }

 private:
  int expandPalindromeLength(string &s, int n, int l, int r) {
    while (l >= 0 && r <= n && s[l] == s[r]) {
      --l;
      ++r;
    }
    return (--r) - (++l) + 1;  // r - l - 1
  }
};
```