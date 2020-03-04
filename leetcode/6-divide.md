##### 括号生成 [22](https://leetcode-cn.com/problems/generate-parentheses/)

#####  Pow(x, n) [50](https://leetcode-cn.com/problems/powx-n/)
```go
func myPow(x float64, n int) float64 {
    if n < 0 {
        x = 1 / x
        n  = -n
    }
    return fastPow(x, n)
}

func fastPow(x float64, n int) float64 {
    if n == 0 {
        return 1.0
    }

    half := fastPow(x, n / 2)

    if (n % 2 == 0) {
        return half * half
    } else {
        return half * half * x
    }
}
```
##### 子集 [78](https://leetcode-cn.com/problems/subsets/)

递归， golang slice 顺序不对，无法通过
```go
func subsets(nums []int) [][]int {
    res := make([][]int, 0)
    do(nums, 0, []int{}, &res)
    return res
}

func do(nums []int, index int, sub []int, res *[][]int) {
    if index == len(nums) {
        *res = append(*res, sub)
        return
    }

    do(nums, index + 1, sub, res)

    sub = append(sub, nums[index])
    do(nums, index + 1, sub, res)
}
```

循环
```go
func subsets(nums []int) [][]int {
	res := make([][]int, 0, 0)
	res = append(res, []int{})

	for _, num := range nums {
		sets := res
		for _, sub := range sets {
			temp := make([]int, len(sub))
			copy(temp, sub)
			res = append(res, append(temp, num))
		}
	}

	return res
}
```

##### [牛顿迭代法原理](http://www.matrix67.com/blog/archives/361)

##### [牛顿迭代法代码](http://www.voidcn.com/article/p-eudisdmk-zm.html)

##### 多数元素 [169](https://leetcode-cn.com/problems/majority-element/description/)

```go
// 分治
func majorityElement(nums []int) int {
	return do(nums, 0, len(nums)-1)
}

func do(nums []int, lo, hi int) int {
	if lo >= hi {
		return nums[lo]
	}

	mid := (hi-lo)/2 + lo

	left := do(nums, lo, mid)
	right := do(nums, mid+1, hi)

	if left == right {
		return left
	}

	leftCount := count(nums, left, lo, hi)
	rightCount := count(nums, right, lo, hi)

	if leftCount > rightCount {
		return left
	}

	return right
}

func count(nums []int, num, lo, hi int) int {
	count := 0

	for lo <= hi {
		if nums[lo] == num {
			count++
		}
		lo++
	}

	return count
}

```
```go
// 摩尔计数
func majorityElement(nums []int) int {
		cur, count := 0, 0
	for _, v := range nums {
		if count == 0 {
			cur = v
		}

		if cur == v {
			count++
		} else {
			count--
		}
	}
	return cur
}
```
##### 电话号码的字母组合 [17](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)
```go
func letterCombinations(digits string) []string {
	m := []string{"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"}
	res := make([]string, 0)

	if digits == "" {
		return res
	}

	do(digits, m, &res, "", 0)
	return res
}

func do(digits string, m []string, res *[]string, sub string, index int) {
	if len(sub) == len(digits) {
		*res = append(*res, sub)
		return
	}

	num, _ := strconv.Atoi(string(digits[index]))
	for _, s := range m[num] {
		do(digits, m, res, sub+string(s), index+1)
	}
}
```
##### N 皇后 [51](https://leetcode-cn.com/problems/n-queens/)

```go
// 代码待优化
func solveNQueens(n int) [][]string {
	res := make([][]string, 0)
	sub := make([]int, 0)

	clus, pies, nas := make(map[int]bool), make(map[int]bool), make(map[int]bool)
	do(n, &res, sub, clus, pies, nas, 0)

	return res
}

func do(n int, res *[][]string, sub []int, clus, pies, nas map[int]bool, row int) {
	if row >= n {
		arr := make([]string, 0)
		for _, q := range sub {
			s := ""
			for i := 0; i < n; i++ {
				if i == q {
					s += "Q"
					continue
				}

				s += "."
			}

			arr = append(arr, s)
		}

		*res = append(*res, arr)
		return
	}

	for clu := 0; clu < n; clu++ {
		if clus[clu] || pies[(row+clu)] || nas[(row-clu)] {
			continue
		}

		clus[clu] = true
		pies[row+clu] = true
		nas[row-clu] = true

		i := clu
		arr := append(sub, i)
		do(n, res, arr, clus, pies, nas, row+1)

		clus[clu] = false
		pies[row+clu] = false
		nas[row-clu] = false
	}

}
```

```go
func reject(c [][]rune, row, col int) bool {
	for i := 0; i < col; i++ {
		if c[row][i] == 'Q' {
			return true
		}
	}

	for i, j := row, col; i >= 0 && j >= 0; {
		if c[i][j] == 'Q' {
			return true
		}
		i--
		j--
	}

	for i, j := row, col; i < len(c) && j >= 0; {
		if c[i][j] == 'Q' {
			return true
		}
		i++
		j--
	}
	return false
}

func solveNQueens1(n int) [][]string {
	var result [][]string

	board := make([][]rune, n)
	for i := range board {
		board[i] = make([]rune, n)
		for j := range board[i] {
			board[i][j] = '.'
		}
	}

	backtracking(&result, board, n, 0)
	return result
}
func backtracking(res *[][]string, board [][]rune, n, column int) {
	// accept
	if n == 0 {
		var arr []string
		for _, v := range board {
			arr = append(arr, string(v))
		}
		*res = append(*res, arr)
		return
	}

	// next
	for i := 0; i < len(board); i++ {
		// reject
		if !reject(board, i, column) {
			board[i][column] = 'Q'
			backtracking(res, board, n-1, column+1)
			board[i][column] = '.'
		}
	}
}

```

```
// 推荐代码
def solveNQueens(self, n):
    def DFS(queens, xy_dif, xy_sum):
        p = len(queens)
        if p==n:
            result.append(queens)
            return None
        for q in range(n):
            if q not in queens and p-q not in xy_dif and p+q not in xy_sum: 
                DFS(queens+[q], xy_dif+[p-q], xy_sum+[p+q])  
    result = []
    DFS([],[],[])
    return [ ["."*i + "Q" + "."*(n-i-1) for i in sol] for sol in result]
```