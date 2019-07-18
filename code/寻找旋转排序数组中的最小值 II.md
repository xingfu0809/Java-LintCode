#### 假设一个旋转排序的数组其起始位置是未知的（比如**0 1 2 4 5 6 7** 可能变成是**4 5 6 7 0 1 2**）。你需要找到其中最小的元素。





[find-minimum-in-rotated-sorted-array-ii](https://www.lintcode.com/problem/find-minimum-in-rotated-sorted-array-ii/description)

```java
样例 
输入 :[2,1]
输出 : 1

输入 :[4,4,5,6,7,0,1,2]
输出: 0

思路1、直接 for 遍历求最小值


思路2、使用二分查找求最小值

  


```

```java
public class Solution {
     /**
     * @param nums: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] nums) {
        // write your code here
        
        int min = Integer.MAX_VALUE;
        for (int i : nums) {
            min = Math.min(min, i);
        }
        return min;
    
    }
}

```

```java

public class Solution {
     
    public int findMin(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int start = 0;
        int end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == nums[end]) {
                // 可能出现 1，1，-1，1，1的情况
                start++;
            } else if (nums[mid] < nums[end]) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (nums[start] <= nums[end]) {
            return nums[start];
        }
        return nums[end];
    }
}



```

