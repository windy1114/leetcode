### 最后一个单词的长度

给你一个字符串 s，由若干单词组成，单词之间用空格隔开。返回字符串中最后一个单词的长度。如果不存在最后一个单词，请返回 0。

单词 是指仅由字母组成、不包含任何空格字符的最大子字符串。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/length-of-last-word


### 解题思路一 借助数组

#### 注意实现
- 前导空客开始
- 末尾空格

1. 将首尾的空格去掉
2. 将输入的字符串转为数组，取最后一个数组元素的长度

```

```
### 解题思路二 从末尾匹配
1. 去掉首尾的空格
2. 从末尾匹配，遇到空格，跳出循环。

```JavaScript
    lengthOfLastWord = function(s) {
      s = s.trim();
      if (!s) return 0;
      let l = s.length;
      for (let i = l - 1; i >= 0; i--) {
        if (s[i] === ' ') {
          return l - i - 1
        }
      }
      return l
    }
```