#### 给定一个32位整数**n**，用同样的数字组成新的32位整数，使得它要比**n**大，返回最小的这样的数。如果不存在这样的整数，返回-1。





[next-greater-element-iii](https://www.lintcode.com/problem/next-greater-element-iii/description)

### **样例**

**样例 1:**

```java
输入: 12
输出: 21
```

**样例 2:**

```java
输入: 21
输出: -1
```

**样例 3:**

```java
输入: 1358431
输出: 1381345
```



**思路**

```java
根据题意以及样例可以看出，5 的位置变成了后面比他大的 8 ，此时 8 后吗的数字变成了升序的 1345 
```





**解法**

```java

public class Solution {
    /**
     * @param n: an integer
     * @return: the smallest 32-bit integer which has exactly the same digits existing in the integer n and is greater in value than n
     */
    public int nextGreaterElement(int n) {
        // Write your code here
        char[] array = String.valueOf(n).toCharArray();
        int len = array.length;
        int index = len - 1;
        while (index > 0) {
            if (array[index - 1] >= array[index]) {
                --index;
            } else {
                break;
            }
        }
        if (index == 0) {
            return -1;
        }
        for (int i = len - 1; i >= index; i--) {
            if (array[i] > array[index - 1]) {
                swap(array, i, index - 1);
                break;
            }
        }
        Arrays.sort(array, index, len);
        try {
            return Integer.valueOf(String.valueOf(array));
        } catch (NumberFormatException e) {
            return -1;
        }
    }
    
    private void swap(char[] array, int i, int j) {
        char temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }

}
```

