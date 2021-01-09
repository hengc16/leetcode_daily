# Word Ladder



Given two words `beginWord` and `endWord`, and a dictionary `wordList`, return _the length of the shortest transformation sequence from_ `beginWord` _to_ `endWord`, _such that_:

* Only one letter can be changed at a time.
* Each transformed word must exist in the word list.

Return `0` if there is no such transformation sequence.

**Example 1:**

```text
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog", return its length 5.
```

**Example 2:**

```text
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
Output: 0
Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```

### 题意:

给你一个初始word， 一个终点word， 和一个wordlist。

如果通过改变一个字母，让初始word改为wordlist里的任意一个word。问最快能几步从初始word 改变到终点word。

### 思路：

把每个word看做是一个node， 所以在wordlist里能一步操作得到的都视为neighbor

```text
Input: beginWord = "hit", endWord = "cog", 
wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: As one shortest transformation is
 "hit" -> "hot" -> "dot" -> "dog" -> "cog", return its length 5.
                                                         
                                                                                                           
                                                                                                                                                             
                                                                                                                                                                                                                                                                
                                hit 
                                 |
                                hot 
                           /          \
                          dot        lot
                         /  \            \
                       lot   dog         log
                              \            \
                              cog           cog
```

这里可以看出这是一个从root往下找shortest path的题

我们用bfs 一层层找最终word， 如果找到返回当前level。



### Code:

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        //用来做bfs
        Queue<String> q = new LinkedList<>();
        //用来当dictionary
        Set<String> set = new HashSet<>(wordList);
        //自己不需要和自己匹配
        set.remove(beginWord);
        q.add(beginWord);
        int level = 0;
        
        while(!q.isEmpty()) {
            int size = q.size();
            level++;
            for(int i = 0; i < size; i++) {
                String curWord = q.poll();
                //拿出来的如果和endword匹配 我们直接return
                if(curWord.equals(endWord)) {
                    return level;
                }
                //拿到当前word所以的neighbor，一步操作的word
                List<String> neighbors = getNeighbors(curWord);
                for(String neighbor : neighbors) {
                    //对每个neighbor进行匹配，如果是dictionary里的word，我们就把他加入下一层。并把他从dictionary里删掉，防止重复。
                    if(set.contains(neighbor)) {
                        set.remove(neighbor);
                        q.add(neighbor);
                    }
                }
            }
        }
        return 0;
    }
    public List<String> getNeighbors(String word) {
        char[] chars = word.toCharArray();
        List<String> res = new ArrayList<>();
        for(int i = 0; i < chars.length; i++) {
            char temp = chars[i];
            for(char c = 'a' ; c <= 'z'; c++) {
                chars[i] = c;
                String neighbor = new String(chars);
                res.add(neighbor);
            }
            chars[i] = temp;
        }
        return res;
    }
}
```

