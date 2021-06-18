### 罗马数字转整数
https://leetcode-cn.com/problems/roman-to-integer/
罗马数字包含以下七种字符:I，V，X，L，C，D和M。
|字符  | 数值 |
| ---- | ----|
| I    |1    |
| V    |5    |
| X    |10   |
| L    |50   |
| C    |100  |
| D    |500  |
| M    |1000 |

例如， 罗马数字 2 写做II，即为两个并列的 1。12 写做XII，即为X+II。 27 写做XXVII, 即为XX+V+II。
通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做IIII，而是IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为IX。这个特殊的规则只适用于以下六种情况：

I可以放在V(5) 和X(10) 的左边，来表示 4 和 9。
X可以放在L(50) 和C(100) 的左边，来表示 40 和90。
C可以放在D(500) 和M(1000) 的左边，来表示400 和900。
给定一个罗马数字，将其转换成整数。输入确保在 1到 3999 的范围内。

### 解题思路一 映射表
- 1. 将所有可能出现的字符对，映射到为键值对
- 2. 如何长度为1， 那么直接输出对应的值
- 3. 遍历字符串：
  - 3.1 如果是字符'I', 'X', 'C'，那么 'IV','IX','XL','XC','CD','CM'的匹配优先级大于单个字符（'I', 'X', 'C'），
  那么 将 s[i] + s[i+1] 去匹配是否存在，如果存在取它的值，将i 往后移动两位（i = i + 2）；
  如果不存在，取s[i]的值
  - 3.2 如果不是，那么直接取s[i]的值  
```
var romanToInt = function(s) {
    const hash = {
      I: 1,
      IV: 4,
      V: 5,
      X: 10,
      IX: 9,
      XL: 40,
      L: 50,
      XC: 90,
      C: 100,
      CD: 400,
      D: 500,
      CM: 900,
      M: 1000
    }

    if (s.length === 1) {
      return hash[s]
    }

    let result = 0
  
    for ( let i = 0; i < s.length; i++ ) {
      let key = s[i]
      if ( ['I', 'X', 'C'].includes(key) ) {
        let t = key + s[i + 1]
        if ( hash.hasOwnProperty(t) ) {
          //有IV,IX,XC,XL,CD,CM
          result += hash[t]
          i = i + 1
        } else {
          result += hash[key]
        }
      } else {
        result += hash[key]
      }
      
    }
    return result
  };
```
### 解题思路二 非映射表
直接匹配
```JavaScript
var romanToInt = s => {
      let result = 0
      for(let i = 0; i < s.length; i++) {
        switch(s[i]) {
          case 'I':
            if (s[i+1] === 'V') {
              result += 4
              i += 1
            } else if (s[i+1] === 'X') {
              result += 9
              i += 1
            } else {
              result += 1
            }
            break;
          case 'V':
            result += 5
            break;
          case 'X':
            if (s[i+1] === 'L') {
              result += 40
              i += 1
            } else if (s[i+1] === 'C') {
              result = result + 90
              i += 1
            } else {
              result  += 10
            }
            break;
          case 'L':
            result += 50
            break;
          case 'C':
            if (s[i+1] === 'D') {
              result += 400
              i += 1
            } else if (s[i+1] === 'M') {
              result += 900
              i += 1
            } else {
              result += 100
            }
            break;
          case 'D':
            result += 500
            break;
          case 'M':
            result += 1000
            break;
        }
        
      }
      console.log(result)
      return result;
    }
```