# leetcode https://leetcode-cn.com/problems/compress-string-lcci/
字符串压缩。利用字符重复出现的次数，编写一种方法，实现基本的字符串压缩功能。比如，字符串aabcccccaaa会变为a2b1c5a3。若“压缩”后的字符串没有变短，则返回原先的字符串。你可以假设字符串中只包含大小写英文字母（a至z）。 
- "aabcccccaaa" => "a2b1c5a3"
- "abbccd" => "abbccd"

###  解题思路一
- 第一步：压缩字符串； 
- 第二步： 比较压缩后的字符串长度和原字符的长度
第一步分解： 循环字符串，一个current记录当前字符，一个count记录当前字符出现的次数，如果遍历的这个字符S[i]和current不等，那么 result =  result + current + count。 接着开始统计 S[i]出现的次数。 循环结束需要把 current + count 统计到result里
```javaScript
	var compressString = function(S) {
		const len = S.length
		
		if ( len === 0 ) {
			return ""
		}

		let count = 1
		let result = ""
		let current = S[0]

		for (let i = 1; i < S.length; i++ ) {
			if ( S[i] !== current ) {
				result = result + current + count
				current = S[i]
				count = 1
			} else {
				count = count + 1
			}
		}
		result = result + current + count
		
		if ( result.length >= len ) {
			result = S
		}

		return result

	};

	compressString("aabccccc")
	compressString("abbccd")

```
### 解题思路二

利用数组pop, push

``` javaScript
	var compressString2 = S => {
		if ( !S.length ) {
			return S
		}

		let result = []
		let current = S[0]
		let count = 1

		result.push(current, count)

		for ( let i = 1; i < S.length; i++) {
			if ( S[i] === current ) {
				result.pop()
				count = count + 1
				result.push(count)
			} else {
				result.push(S[i], 1)
				current = S[i]
				count = 1
			}
		}

		result = result.join("")

		if (S.length <= result.length) {
			result = S
		}

		return result;
	}

	compressString2("aabccccc");
```