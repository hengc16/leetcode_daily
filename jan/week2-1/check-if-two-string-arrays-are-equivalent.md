# Check If Two String Arrays are Equivalent



Given two string arrays `word1` and `word2`, return __`true` _if the two arrays **represent** the same string, and_ `false` _otherwise._

A string is **represented** by an array if the array elements concatenated **in order** forms the string.

**Example 1:**

```text
Input: word1 = ["ab", "c"], word2 = ["a", "bc"]
Output: true
Explanation:
word1 represents string "ab" + "c" -> "abc"
word2 represents string "a" + "bc" -> "abc"
The strings are the same, so return true.
```

**Example 2:**

```text
Input: word1 = ["a", "cb"], word2 = ["ab", "c"]
Output: false
```

**Example 3:**

```text
Input: word1  = ["abc", "d", "defg"], word2 = ["abcddefg"]
Output: true
```

### 思路:

想了半天找space O\(1\)的解法， 然而并没有。 那如果可以用space O\(n\). 把array里的element连接起来，再对比就好了。

### Code

```java
class Solution {
    public boolean arrayStringsAreEqual(String[] word1, String[] word2) {
        return (String.join("",word1).equals(String.join("",word2)));
    }
}
```

