#### 设计一个算法，找出只含素因子`2`，`3`，`5` 的第 *n* 小的数。

#### 符合条件的数如：`1, 2, 3, 4, 5, 6, 8, 9, 10, 12...`

[ugly-number-ii](https://www.lintcode.com/problem/ugly-number-ii/description)



### **样例**

**样例 1：**

```java
输入：9
输出：10
```

**样例 2：**

```java
输入：1
输出：1
```

```java
分析：假设数组ugly[N]中存放不断产生的丑数，初始只有一个丑数ugly[0]=1，由此出发，下一个丑数由因子2,3,5竞争产生，得到ugly[0]*2, ugly[0]*3, ugly[0]*5， 显然最小的那个数是新的丑数，所以第2个丑数为ugly[1]=2，开始新一轮的竞争，由于上一轮竞争中，因子2获胜，这时因子2应该乘以ugly[1]才显得公平，得到ugly[1]*2,ugly[0]*3,ugly[0]*5， 因子3获胜，ugly[2]=3，同理，下次竞争时因子3应该乘以ugly[1]，即：ugly[1]*2, ugly[1]*3, ugly[0]*5, 因子5获胜，得到ugly[3]=5，重复这个过程，直到第n个丑数产生。总之：每次竞争中有一个（也可能是两个或三个）因子胜出，下一次竞争中 胜出的因子就应该乘下一个数。

```





```java
public class Solution {
    /**
     * @param n: An integer
     * @return: return a  integer as description.
     */
    public int nthUglyNumber(int n) {
        // write your code here
        
        int i = 0;
        int j = 0;
        int k = 0;
        int index = 1;
        int[] dp = new int[n];
        dp[0] = 1;
        while (index < n) {
            dp[index] = Math.min(Math.min(dp[i] * 2, dp[j] * 3), dp[k] * 5);

            if (dp[index] == dp[i] * 2) {
                i++;
            }
            if (dp[index] == dp[j] * 3) {
                j++;
            }
            if (dp[index] == dp[k] * 5) {
                k++;
            }
            index++;
        }
        return dp[n - 1];
    }
}
```



