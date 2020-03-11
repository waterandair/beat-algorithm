##### 转换成小写字母 [709](https://leetcode-cn.com/problems/to-lower-case/)
```go
func toLowerCase(str string) string {
	runes := []rune(str)
	diff := 'a'-'A'
	for i, v := range runes {
		if v >= 'A' && v <= 'Z' {
			runes[i] = v + diff
		}
	}

	return string(runes)
}
```

```go
func toLowerCase(str string) string {
	runes := []rune(str)
	for i, _ := range runes {
		runes[i] |= 32
	}

	return string(runes)
}
```

##### 最后一个单词的长度 [58](https://leetcode-cn.com/problems/length-of-last-word/)

```go
func lengthOfLastWord(s string) int {
    tail := len(s) - 1
    for tail >= 0 && s[tail] == ' ' {
        tail --
    }

    length := 0
    for tail >= 0 && s[tail] != ' ' {
        length ++
        tail --
    }

    return length
}
```

##### 字符串中的第一个唯一字符 [387](https://leetcode-cn.com/problems/first-unique-character-in-a-string/)
```go
func firstUniqChar(s string) int {
	arr := [26]uint64{}
	for _, v := range s {
		arr[v - 'a']++
	}
	
	for i, v := range s {
		if arr[v-'a'] == 1 {
			return i
		}
	} 
	
	return -1
}
```

```go
func firstUniqChar(s string) int {
	// 下标索引, 26个slot. 初始化为-1
	indexes := make([]int, 26)
	for i, _ := range indexes {
		indexes[i] = -1
	}

	length := len(s)

	// 记录下标, 重复出现的字符下标索引置为字符串长度
	for i, v := range s {
		offset := v - 'a'
		if indexes[offset] == -1 {
			indexes[offset] = i
		} else {
			indexes[offset] = length
		}
	}

	// 查找下标索引中下标最小的, 循环26次, 与字符串长度无关.
	// 字符串超长, 且只出现一次的字符出现在末尾时, 遍历次数 >> 26
	firstIndex := length
	for _, index := range indexes {
		if (index > -1 && index < length) && index < firstIndex {
			firstIndex = index
		}
	}
	if firstIndex == length {
		return -1
	}
	return firstIndex
}
```

##### 字符串转换整数 (atoi) [8](https://leetcode-cn.com/problems/string-to-integer-atoi/)

```go
func myAtoi(str string) int {
	res, sign, length, idx := 0, 1, len(str), 0

	// Skip leading spaces
	for idx < length && (str[idx] == ' ' || str[idx] == '\t') {
		idx++
	}

	// +/- Sign
	if idx < length {
		if str[idx] == '+' {
			sign = 1
			idx++
		} else if str[idx] == '-' {
			sign = -1
			idx++
		}
	}

	// Numbers
	for idx < length && str[idx] >= '0' && str[idx] <= '9'{
		res = res * 10 + int(str[idx]) - '0'
		if sign * res > math.MaxInt32 {
			return math.MaxInt32
		} else if sign * res < math.MinInt32 {
			return math.MinInt32
		}
		idx++
	}

	return res * sign
}
```

##### 最长公共前缀 [14](https://leetcode-cn.com/problems/longest-common-prefix/)
```go
func longestCommonPrefix(strs []string) string {
    if len(strs) == 0 {return ""}
    if len(strs) == 1 {return strs[0]}
    mx := 0
    for {
        for i := 1; i < len(strs); i++ {
            if mx >= len(strs[i-1]) || mx >= len(strs[i]) || strs[i-1][mx] != strs[i][mx] {
                return strs[0][:mx]
            }
        }
        mx++
    }
}
```

##### 反转字符串 [344](https://leetcode-cn.com/problems/reverse-string/)
```go
func reverseString(s []byte) {
	for i, j:= 0, len(s) - 1; i < j; i++ {
		s[i], s[j] = s[j], s[i]
		j -- 
	}
}
```
##### 反转字符串2 [541](https://leetcode-cn.com/problems/reverse-string-ii/)


##### 翻转字符串里的单词 [151](https://leetcode-cn.com/problems/reverse-words-in-a-string/)

##### 反转字符串中的单词 III [557](https://leetcode-cn.com/problems/reverse-words-in-a-string-iii/)


##### 仅仅反转字母[917](https://leetcode-cn.com/problems/reverse-only-letters/)

