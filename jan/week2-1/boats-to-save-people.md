# Boats to Save People

The `i`-th person has weight `people[i]`, and each boat can carry a maximum weight of `limit`.

Each boat carries at most 2 people at the same time, provided the sum of the weight of those people is at most `limit`.

Return the minimum number of boats to carry every given person.  \(It is guaranteed each person can be carried by a boat.\)



**Example 1:**

```text
Input: people = [1,2], limit = 3
Output: 1
Explanation: 1 boat (1, 2)
```

**Example 2:**

```text
Input: people = [3,2,2,1], limit = 3
Output: 3
Explanation: 3 boats (1, 2), (2) and (3)
```

**Example 3:**

```text
Input: people = [3,5,3,4], limit = 5
Output: 4
Explanation: 4 boats (3), (3), (4), (5)
```

### 思路

首先每个person guarantee can be carried by a boat.

那如果person array是有序的。 我们就可以尝试让当前最轻的和最重的匹配。

* 如果最重的加最轻的超出了limit，
  * 也就代表了在person里，如果最轻的都不能和最重的匹配，那不可能有人比最轻的还轻，最重的只能一个人做船了 
* 如果最轻的和最重的匹配成功
  * 我们左边界右移， 右边界左移， 继续下次匹配。

### Code:

```java
class Solution {
    public int numRescueBoats(int[] people, int limit) {
        Arrays.sort(people);
        int l = 0;
        int r = people.length - 1;
        int res = 0;
        while(l <= r) {
            if((people[l] + people[r]) <= limit) {
                l++;
                r--;
                res++;
            }else{
                r--;
                res++;
            }
        }
        return res;
    }
}
```

