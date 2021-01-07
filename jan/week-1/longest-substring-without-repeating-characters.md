# Longest Substring Without Repeating Characters



Given a string `s`, find the length of the **longest substring** without repeating characters.

**Example 1:**

```text
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

**Example 2:**

```text
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**

```text
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

### 思路:

用sliding window, 2个指针，left 和 right， \[left, right\] 之间不能有重复。 

用一个hashmap 来记录element 和对应的index。

当right指针遇到map里重复的元素时：

更新globalmax， 和左边框。

abca

当right = 3 的时候， 发现重复， 这是要将 左边框更新为 1， 也就是新的substring 从b开始。

abbabc

当right = 3 的时候， 发现重复，这里如果我们只是单纯的提取a在map对应的value， 会发现，我们又回到了index 1。 可是index1 和index2 都是b， 是handle过得case。为了避免这种事发送，我们可以取Max\(left, map.get\(arr\[right\]\)\)， 保证重复值在当前window里。

### Code:

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int l = 0;
        int r = 0;
        int max = 0;
        while( r < s.length()) {
            if(map.containsKey(s.charAt(r))){
                l = Math.max(map.get(s.charAt(r)),l);
            }
            max = Math.max(max, r - l + 1);
            map.put(s.charAt(r), r + 1);
            r++;
        }
        return max;
    }
}
```

