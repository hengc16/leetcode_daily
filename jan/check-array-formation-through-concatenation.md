# Check Array Formation Through Concatenation

You are given an array of **distinct** integers `arr` and an array of integer arrays `pieces`, where the integers in `pieces` are **distinct**. Your goal is to form `arr` by concatenating the arrays in `pieces` **in any order**. However, you are **not** allowed to reorder the integers in each array `pieces[i]`.

Return `true` _if it is possible to form the array_ `arr` _from_ `pieces`. Otherwise, return `false`.

**Example 1:**

```text
Input: arr = [85], pieces = [[85]]
Output: true
```

**Example 2:**

```text
Input: arr = [15,88], pieces = [[88],[15]]
Output: true
Explanation: Concatenate [15] then [88]
```

**Example 3:**

```text
Input: arr = [49,18,16], pieces = [[16,18,49]]
Output: false
Explanation: Even though the numbers match, we cannot reorder pieces[0].
```

**Example 4:**

```text
Input: arr = [91,4,64,78], pieces = [[78],[4,64],[91]]
Output: true
Explanation: Concatenate [91] then [4,64] then [78]
```

**Example 5:**

```text
Input: arr = [1,3,5,7], pieces = [[2,4,6,8]]
Output: false
```

### 题意：

* 给你2个array
  * arr 里装的都是distinct的element，也就是无重复的
  * pieces里装的suppose是arr的subarry， 如果不是返回false。
* return true 如果可以通过切片来拼成arr

### 思路:

since pieces里装的都是切块

建一个hashmap， key为切块的头，value为整个切块

iterate整个pieces array， 把切块的头和切块放入hashmap里

iterate 整个arr， 

* check hashmap是否有当前element
  * 没有 直接return false， 拼不成
  * 如果有
    * 因为是subarray，所以也要检查完整切片是否和当前element后续部分吻合
      * 如果吻合继续
      * 如果不吻合 return false， 因为题目中不让reorder

### Code：

```java
class Solution {
    public boolean canFormArray(int[] arr, int[][] pieces) {
        Map<Integer, int[]> map  = new HashMap<>();
        for(int[] piece : pieces) {
            map.put(piece[0], piece);
        }
        int i = 0;
        while(i < arr.length) {
            if(!map.containsKey(arr[i])) return false;
            int[] piece = map.get(arr[i]);
            for(int p : piece) {
                if(arr[i] != p) return false;
                i++;
            }
        }
        return true;
    }
}
```





