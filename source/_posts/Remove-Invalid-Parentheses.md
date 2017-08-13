---
title: Remove Invalid Parentheses
date: 2016-10-20 17:12:44
tags: LeetCode
---

### **写在前面**
今天跟儿时玩伴乐聊天了解到了[OJ(Online Judge)][1]，简单寒暄几句就是聊工作，本来还是他问我[GDAL][2]的，我也是第一次听说，待后续继续了解。从聊天中我收获的就是除了OJ之外，还有就是应该对自己平常的工作有一总结，不管有没有人看，都把它记录下来，一直就觉得这个习惯还是蛮重要的，知识不总结很快就容易遗忘，所以今晚开始（2016/10/20晚22:00）尽可能坚持这种习惯，并要将之前的工作和收获都记录下来，为工作也是为未来铺垫。

### **Question** 
       Remove the minimum number of invalid parentheses in order to make the input string valid. And return all possible results.

### **Examples**
    "()())()" -> ["()()()", "(())()"]
    "(a)())()" -> ["(a)()()", "(a())()"]
    ")(" -> [""]
**Tag:**     Depth-first Search、Breadth-first Search
**Similar Problem:** [Valid Parentheses][3]

### **Solution**
From [StefanPochmann][4]:
```python
def remove_invalid_parentheses(s):
    # Once the count of ')' is more than '(' first appeared , the cycle will be exit instantly.
    # But if cycle over normally, the count of '(' is not less than ')'
    # To judge whether the 's' is valid
    def isvalid(s):
        ctr = 0
        for c in s:
            if c == '(':
                ctr += 1
            elif c == ')':
                ctr -= 1
                if ctr < 0:
                    return False
        # It contains a condition judgment that if ctr is 0 then returns True, or returns False.
        return ctr == 0

    # Transforming 's' into a Set
    level = {s}
    i = 0   # To store the cycle count
    while True:
        i = i + 1
        # Calling function 'filter' and return a list containing valid results
        valid = filter(isvalid, level)
        if valid:
            print i
            return valid   # This is the only one exit of this function and return a valid result(List)
        # 'level' is used to store all possible assembly after removing one invalid parentheses.
        level = {s[:i] + s[i+1:] for s in level for i in range(len(s))}
        print level


if __name__ == "__main__":
    ss = "()()()"
    # It's used to accept valid results
    valid = remove_invalid_parentheses(ss)
    print valid

```
---

**思路：**首先需要写一个判断函数（isvalid），就是对每个括号组合都需要进行判断，只有在遍历每个括弧时，遍历过程中不能出现')'的数量比'('的数量先多，若有此情况则跳出循环，无需再做后续判断；但是反之是可以的，且在此情况下一直遍历到最后一个括弧符号，当'('和')'的数量相等，则一定是满足条件的括弧组合，也是**唯一的条件**，反之数量不等，即'('的数量比')'的数量多，则也不满足条件。其次要完成移除一个字符，使用了列表生成式*s[:i] + s[i+1:] for s in level for i in range(len(s))*。最后就是循环对每个移除掉一个字符的括弧组合进行有效性检验，并且返回有效的组合。

**附：**
>1. 列表生成式的使用，能节省很多的循环的嵌套；
>2. filter(function, sequence)函数的使用，返回的是满足函数条件的sequence中的元素，并以List/Tuple/string类型返回；
>3. return ctr==0，该语句既实现了条件判断，也返回了值。

**后记：**这个程序自己怎么都想不出来，还是看了别人的代码，然后自己一点一点理解，到今天（10.31日晚）才吃透。看来想学习算法，上来就啃难的不适合我这种智商不够的。
自己的理解都写在注释里，感觉蛮凌乱的，后面学习过程中一定要注意注释也要简介，否则篇幅过长也影响程序整体的简洁。
  [1]: https://leetcode.com/
  [2]: http://baike.baidu.com/link?url=xgSZX3a852uGeTzsOJr8rB6EX2oP4rO8C5KbqcNTXq-GHxnMoKEZrk5KmtS63g9QuJG6_0HlkOXwJS6h3o64ja
  [3]: https://leetcode.com/problems/valid-parentheses/
  [4]: https://discuss.leetcode.com/topic/28833/short-python-bfs