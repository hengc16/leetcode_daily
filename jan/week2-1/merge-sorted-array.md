# Merge Sorted Array



Given two sorted integer arrays `nums1` and `nums2`, merge `nums2` into `nums1` as one sorted array.

The number of elements initialized in `nums1` and `nums2` are `m` and `n` respectively. You may assume that `nums1` has enough space \(size that is equal to `m + n`\) to hold additional elements from `nums2`.

**Example 1:**

```text
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
```

**Example 2:**

```text
Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
```

### Code

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int right = nums1.length - 1;
        m--;
        n--;
        while(m >= 0 || n >= 0) {
            if(n < 0) {
                nums1[right--] = nums1[m--];
            }else if( m < 0) {
                nums1[right--] = nums2[n--];
            }
            else if(nums2[n] > nums1[m]) {
                nums1[right--] = nums2[n--];
            }else{
                nums1[right--] = nums1[m--];
            }
        }
    }
}
```

