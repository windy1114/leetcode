### 验证回文串

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。
输入: "A man, a plan, a canal: Panama"
输出: true

来源： https://leetcode-cn.com/problems/valid-palindrome/

### 解题思路一 利用数组reverse 

1. 遍历字符串，逐个判断是否字母，数字，并且统一大小写，压缩栈中 
2. 字符串本身是否等于字符串的逆序（利用数组reverse求出反串）

```
  var isPalindrome = function(s) {
    // ""A man, a plan, a canal: Panama""
    // 不区分大小写
    // 只处理字母数字

    let result = []
    for (let i = 0; i < s.length; i++) {
      if (/[A-Z|a-z|\d]/.test(s[i])) {
        result.push(s[i].toLowerCase())
      }
    }
    
    s = [...result]
    s = s.reverse().join("")
    result = result.join("")
    return result === s
  };
```
### 解题思路二 首尾指针

1. 考虑到中间空格，大小写问题，用正则修改原字符串，去掉非字母数字
2. 首尾比较，往中间扩散。 统一大小写比较是否相等；如果不相等那么，说明不是回文 return false； 如果一直相等，首尾指针相遇，那么说明是回文串

```JavaScript
var isPalindrome = function (s) {
    //双指针
    s = s.replace(/[^a-zA-Z0-9]/g, "")
    for (let i = 0, j = s.length - 1; i < j; i++) {
      if ( (s[i].toLowerCase() === s[j].toLowerCase() ) ) {
        j = j - 1;
      } else {
        return false
      }
    }

    return true
  }
```