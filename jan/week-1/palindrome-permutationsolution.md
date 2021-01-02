# Palindrome PermutationSolution



Given a string, determine if a permutation of the string could form a palindrome.

**Example 1:**

```text
Input: "code"
Output: false
```

**Example 2:**

```text
Input: "aab"
Output: true
```

**Example 3:**

```text
Input: "carerac"
Output: true
```

### 题意：

给你个string， 问它的permutation里有没有palindrome。

### 思路：

aabb, aabaa, a, baaab 都为palindrome， 要想符合palindrome，只有中间的那个数可以是奇数，其他的都是对称的，也就是出现必然是成对出现，也就是偶数。

那我们把这个string每个字母出现的次数存在hashmap里， 如果出现2个字母或2个字母以上为奇数，那它必然不是palindrome。

### code:

```java
class Solution {
    public boolean canPermutePalindrome(String s) {
        Map<Character, Integer> map = new HashMap<>();
        for(char c : s.toCharArray()) {
            int count = map.getOrDefault(c, 0);
            map.put(c, count + 1);
        }
        boolean flag = false;
        for(int i : map.values()) {
            if(flag && (i % 2 != 0)) {
                return false;
            }
            if(i % 2 != 0) {
                flag = true;
            }
        }
        return true;  
    }
}
```

