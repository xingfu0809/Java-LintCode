#### 在Dota2的世界中，有两个党派：Radiant和Dire。

#### Dota2参议院由来自两党的参议员组成。现在，参议院想要对Dota2游戏的变化做出决定。对此变化的投票是基于回合的。在每一回合中，每位参议员都可以行使以下两项权利之一：

#### 禁止一位参议员的权利：
一个参议员可以让另一位参议员在这次以及随后的所有回合中失去所有投票权。

#### 宣布胜利：
如果这位参议员发现仍然有投票权的参议员都来自同一方，他可以宣布胜利并做出关于比赛变化的决定。

#### 给出代表每个参议员所属党派的字符串。字符“R”和“D”分别代表Radiant方和Dire方。然后，如果有n个参议员，则给定字符串的大小将为n。

#### 基于回合的过程从给定顺序的第一个参议员到最后一个参议员开始。此程序将持续到投票结束。在这个过程中，所有失去投票权的参议员都将被跳过。

#### 假设每个参议员足够聪明并且将为自己的政党发挥最佳策略，你需要预测哪一方最终宣布胜利并使Dota2比赛进行改变。输出应为Radiant或Dire。

```java
给出的字符串长度范围为[1, 10,000]。
```



[dota2-senate](https://www.lintcode.com/problem/dota2-senate/description)



### **样例**

**样例 1:**

```java
输入: 
RD
输出: 
Radiant

解释:
第一个参议员来自Radiant ，他可以禁止下一个参议员在第一轮的权利。
第二个参议员不能再行使任何权利，因为他的权利已经被禁止了。
在第二轮选举中，第一个参议员可以宣布胜利，因为他是参议院中唯一可以投票的人。
```

**样例 2:**

```java
输入: 
RDD
输出:
Dire

解释: 
第一位参议员来自Radiant，他可以在第一回合中禁止下一位参议员的权利。
由于他的权利被禁止，第二位参议员不再行使任何权利。
第三位参议员来自Dire，他可以在第一回合禁止第一位参议员的权利。
在第二回合中，第三位参议员可以宣布胜利，因为他是参议院中唯一可以投票的人。
```



**思路**

```
这道题是很明显的贪心算法的
R必会首先ban随后第一个D，同理D必会首先ban随后的第一个R
这里维护R和D两个队列，每次挑R和D的队首PK，胜利的一方加n（下一轮继续PK），无论胜利还是失败这一轮都需要pop出来
```



```java
public class Solution {
    /**
     * @param senate: a string
     * @return: return a string
     */
    public String predictPartyVictory(String senate) {
        // write your code here
        Queue<Integer> rQueue = new LinkedList<>();
        Queue<Integer> dQueue = new LinkedList<>();
        int length = senate.length();
        for (int i = 0; i < length; i++) {
            if (senate.charAt(i) == 'R') {
                rQueue.offer(i);
            } else {
                dQueue.offer(i);
            }
        }
        while (!rQueue.isEmpty() && !dQueue.isEmpty()) {
            int rIndex = rQueue.poll();
            int dIndex = dQueue.poll();
            if (rIndex > dIndex) {
                dQueue.offer(dIndex + length);
            } else {
                rQueue.offer(rIndex + length);
            }
        }
        return rQueue.isEmpty() ? "Dire" : "Radiant";
    }
}
```

