//匹配左括号，是左括号那么入栈，如果不是，那么判断是否和栈顶的左括号匹配，不匹配，说明不是有效的符号
```
var isValid = function(s) {
if (s.length % 2 === 1) return false;
  const hashMap = {
    "(": ")",
    "[": "]",
    "{": "}"
  }
  let arr = []
  for (let i = 0; i < s.length; i++) {
    if (hashMap.hasOwnProperty(s[i])) {
      arr.push(s[i])
    } else {
      let l = arr.length
      let t = arr[l - 1]
      //是右括号 并且匹配了,出栈
      if (hashMap[t] === s[i]) {
        arr.pop()
      } else {
        return false
      }
    }
  }
  return !arr.length
};
```
