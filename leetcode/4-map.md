##### 有效的字母异位词 [242](https://leetcode-cn.com/problems/valid-anagram/description/)
```go
    if len(s)!=len(t){
		return false
	}
	v:=make([]int,26)
	for i:=0;i< len(s);i++{
		v[s[i]-'a']++
		v[t[i]-'a']--
	}
	for i:=0;i<26;i++{
		if v[i]!=0{
			return false
		}
	}
	return true
```

##### 字母异位词分组 [49](https://leetcode-cn.com/problems/group-anagrams/)
```go

func groupAnagrams(strs []string) [][]string {
	m := make(map[string][]string)

	for _, v := range strs {
		b := []byte(v)
		sort.Slice(b, func(i, j int) bool {
			return b[i] < b[j]
		})

		k := string(b)
		m[k] = append(m[k], v)
	}

	res := make([][]string, 0)
	
	for _, v := range m {
		arr := make([]string, 0)
		for _, s := range v {
			arr = append(arr, s)
		}

		res = append(res, arr)
	}

	return res
}
```

```go
func groupAnagrams(strs []string) [][]string {
    dict := make(map[[26]int][]string)
    for _,s := range strs {
        k := getKey(s)
        dict[k] = append(dict[k],s)
      
    }
    var res [][]string
    for _,v := range dict {
        res = append(res,v)
    }
    return res
}

func getKey(s string) [26]int {
    var k [26]int
    for i := range s {
        k[int(s[i]-'a')]++
    }
    return k
}
```


##### 两数之和 [1](https://leetcode-cn.com/problems/two-sum/description/)