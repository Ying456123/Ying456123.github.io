---
published: false
---
# **Sliding Window**

滑动窗口(Sliding Window)问题经常使用快慢指针(slow, fast pointer)

[0, slow) 的区域为滑动窗口已经探索过的区域
[slow, fast]的区域为滑动窗口正在探索的区域
(fast, end of array)为待探索的区域
Sliding Window的问题主要分为:

**fixed size sliding window**

**dynamic size sliding window**


 先来看看fixed size sliding window相关的问题

１.Strstr:
Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.
Input: haystack = "hello", needle = "ll"
Output: 2


```
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if needle == '':
            return 0
        l = len(needle)
        for i in range(len(haystack)-len(needle)+1):
            if haystack[i:i+l] == needle:
                return i
                break
        return -1
```
 2.Repeated DNA Sequennce
All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.
Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.
Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",
Return:
["AAAAACCCCC", "CCCCCAAAAA"]
```
class Solution(object):
    def findRepeatedDnaSequences(self, s):
        """
        :type s: str
        :rtype: List[str]
        """
        seen, repeated = set(), set()
        for i in range(len(s)-9):
            t = s[i:i+10]
            if t in seen:
                repeated.add(t)
            seen.add(t)
        return list(repeated)
```
接下来看看Non-fixed Size Sliding-Window的例子：

Longest Substring Without Repeating Characters
```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        n = len(s)
        ans = 0
        d = {}
        start = 0
        i = 0
        for j in range(n):
            if s[j] in d and start <= d[s[j]]:
                start = d[s[j]] + 1
            ans = max(ans, j-start+1)
            d[s[j]] = j
        return ans
```
我最开始犯错在于，当检测到重复时，直接把start定位到end，这样肯定是错误的。比如dvdnc,如果直接把start定位到d的话，就会错过v，从而导致没有找到最大子字符串。




