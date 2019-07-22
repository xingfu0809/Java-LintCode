#### 给定一个整型数组，找到主元素，它在数组中的出现次数严格大于数组元素个数的三分之一。

[majority-element-ii](https://www.lintcode.com/problem/majority-element-ii/description)



### **样例**

例1:

```
输入: [99,2,99,2,99,3,3], 
输出: 99.
```

例2:

```
输入: [1, 2, 1, 2, 1, 3, 3], 
输出: 1.
```

#### **思路1**

```java
使用 map 存储每个元素的个数
遍历 map 如果个数大于1/3 返回key 即可

```

#### **思路2[摩尔投票法](https://www.jianshu.com/p/c19bb428f57a)**

```java

在任何数组中，出现次数大于该数组长度 1/3 的值只能有一个。
遍历数组找出出现次数最多的哪两个数，然后在遍历数组算出个数
最后比较个数，返回个数大的元素值

```





```java
public class Solution {
    /*
     * @param nums: a list of integers
     * @return: The majority number that occurs more than 1/3
     */
    public int majorityNumber(List<Integer> nums) {
        // write your code here
        Map<Integer, Double> map = new HashMap<>();
        for (Integer num : nums) {
            map.put(num, map.getOrDefault(num, 0.0) + 1);
        }
        for (Integer key : map.keySet()) {
            if (map.get(key) / nums.size() > 1.0 / 3) {
                return key;
            }
        }
        return -1;
    }
}
```





```java


public class Solution {
   
    /**
     * @param nums: A list of integers
     * @return: The majority number that occurs more than 1/3
     */
    public int majorityNumber(List<Integer> nums) {
        // write your code
        if (nums == null || nums.size() == 0) {
            return -1;
        }

        int num1 = 0;
        int num2 = 0;
        int count1 = 0;
        int count2 = 0;
        for (Integer num : nums) {

            if (count1 == 0) {
                num1 = num;
                count1++;
            } else if (num1 == num) {
                count1++;
            } else if (count2 == 0) {
                num2 = num;
                count2++;
            } else if (num2 == num) {
                count2++;
            } else {
                count1--;
                count2--;
            }
        }

        count1 = 0;
        count2 = 0;
        for (Integer num : nums) {
            if (num == num1) {
                count1++;
            }
            if (num == num2) {
                count2++;
            }
        }

        return count1 > count2 ? num1 : num2;

    }
}
```

