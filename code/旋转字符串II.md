#### 给出一个字符串(以字符数组形式给出)，一个右偏移和一个左偏移，根据给出的偏移量循环移动字符串。(left offest表示字符串向左的偏移量，right offest表示字符串向右的偏移量，左偏移量和右偏移量计算得到总偏移量，在总偏移量处分成两段字符串并交换位置)





[rotate-string-ii](https://www.lintcode.com/problem/rotate-string-ii/description)

```java
样例
样例 1:

输入：str ="abcdefg", left = 3, right = 1
输出："cdefgab"
解释：左偏移量为3，右偏移量为1，总的偏移量为向左2，故原字符串向左移动，变为"cdefg" + "ab"。
样例 2:

输入：str="abcdefg", left = 0, right = 0
输出："abcdefg" 
解释：左偏移量为0，右偏移量为0，总的偏移量0，故字符串不变。
样例 3:

输入：str = "abcdefg",left = 1, right = 2
输出："gabcdef"
解释：左偏移量为1，右偏移量为2，总的偏移量为向右1，故原字符串向右移动，变为"g" + "abcdef"。

题意：看样例知道只是一个字符串的拼接，关键是要分别处理左偏移量大于右偏移量，处理右偏移量大于左偏移量的情况，如果偏移量相等直接返回，值得注意的是偏移量需要对字符串长度取模


```

```java
public class Solution {
    /**
     * @param str: An array of char
     * @param left: a left offset
     * @param right: a right offset
     * @return: return a rotate string
     */
    public String RotateString2(String str, int left, int right) {
        // write your code here
        if (str == null || str.length() == 0 || left == right) {
            return str;
        }
        int len = str.length();
        left %= len;
        right %= len;
       
        if (left > right) {
            int temp = left - right;
            return str.substring(temp) + str.substring(0, temp);
        } else {
            int temp = Math.abs(right - left);
            return str.substring(str.length() - temp) + str.substring(0, str.length() - temp);

        }
    }
}
```

