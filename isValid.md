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
