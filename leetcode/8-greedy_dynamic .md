#### 贪心算法/动态规划

[动态规划](https://zh.wikipedia.org/wiki/动态规划)

[最短路径算法b站视频](https://www.bilibili.com/video/av53233912?from=search&seid=2847395688604491997)

贪心算法适合解决 最小生成树，哈弗曼编码。

##### 柠檬水找零 [860](https://leetcode-cn.com/problems/lemonade-change/description/)

##### 买卖股票的最佳时机 II [122](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/description/)
```go
// 贪心
func maxProfit(prices []int) int {
	max := 0
	for i := 1; i < len(prices); i++ {
		index := i
		if prices[index] > prices[index-1] {
			max += prices[index] - prices[index-1]
		}
	}
	return max
}
```

##### 分发饼干 [455](https://leetcode-cn.com/problems/assign-cookies/description/)
```go
// 贪心
func findContentChildren(g []int, s []int) int {
	sort.Ints(g)
	sort.Ints(s)

	var gi, si int

	for gi < len(g) && si < len(s) {
		if s[si] >= g[gi] {
			gi++
		}
		si++
	}

	return gi
}
```

##### 模拟行走机器人 [874](https://leetcode-cn.com/problems/walking-robot-simulation/description/)


##### 跳跃游戏 [55](https://leetcode-cn.com/problems/jump-game/)
```go
// 可以巧妙的使用贪心
func canJump(nums []int) bool {
	end := len(nums) - 1
	for i := len(nums) - 1; i >= 0; i-- {
		if nums[i]+i >= end {
			end = i
		}
	}

	return end == 0
}
```
##### 跳跃游戏 II [45](https://leetcode-cn.com/problems/jump-game-ii/)

##### 不同路径 [62](https://leetcode-cn.com/problems/unique-paths/)
```go
// 分治 + 缓存

func uniquePaths(m int, n int) int {
	mem := make(map[[2]int]int)
	return do(m, n, 1, 1, mem)
}

func do(m, n, mi, ni int, mem map[[2]int]int) int {
	if mi >= m || ni >= n {
		return 1
	}

	under := 0
	right := 0
	if mem[[2]int{mi + 1, ni}] != 0 {
		under = mem[[2]int{mi + 1, ni}]
	} else {
		under = do(m, n, mi+1, ni, mem)
		mem[[2]int{mi + 1, ni}] = under
	}

	if mem[[2]int{mi, ni + 1}] != 0 {
		right = mem[[2]int{mi, ni + 1}]
	} else {
		right = do(m, n, mi, ni+1, mem)
		mem[[2]int{mi, ni + 1}] = right
	}

	return under + right
}
```

```go
// dp

func uniquePaths(m int, n int) int {
	mem := make([]int, 0)
	for i := 0; i < m; i++ {
		mem = append(mem, 1)
	}

	for ni := n - 2; ni >= 0; ni-- {
		for mi := m - 1; mi >= 0; mi-- {
			i := mi
			if mi == m-1 {
				mem[i] = 1
				continue
			}

			mem[i] = mem[i] + mem[i+1]
		}
	}

	return mem[0]
}
```

##### 不同路径 II [63](https://leetcode-cn.com/problems/unique-paths-ii/)
```go
// 分治 + 缓存
func uniquePathsWithObstacles(obstacleGrid [][]int) int {
	mem := make(map[[2]int]int)
	return do(obstacleGrid, 0, 0, mem)
}

func do(obstacleGrid [][]int, x, y int, mem map[[2]int]int) int {
	if obstacleGrid[y][x] == 1 || x > len(obstacleGrid[0])-1 || y > len(obstacleGrid)-1 {
		return 0
	}

	if x == len(obstacleGrid[0])-1 {
		for i := y; i < len(obstacleGrid); i++ {
			if obstacleGrid[i][x] == 1 {
				return 0
			}
		}
		return 1
	}
	if y == len(obstacleGrid)-1 {
		for i := x; i < len(obstacleGrid[0]); i++ {
			if obstacleGrid[y][i] == 1 {
				return 0
			}
		}
		return 1
	}

	under := 0
	right := 0

	if v, ok := mem[[2]int{x, y + 1}]; ok {
		under = v
	} else {
		under = do(obstacleGrid, x, y+1, mem)
		mem[[2]int{x, y + 1}] = under
	}

	if v, ok := mem[[2]int{x + 1, y}]; ok {
		right = v
	} else {
		right = do(obstacleGrid, x+1, y, mem)
		mem[[2]int{x + 1, y}] = right
	}

	return under + right
}
```

```go
// dp

```

##### 最长公共子序列 [1143](https://leetcode-cn.com/problems/longest-common-subsequence/)
```go
// dp

```

#####  爬楼梯 [70](https://leetcode-cn.com/problems/climbing-stairs/description/)

##### 三角形最小路径和 [120](https://leetcode-cn.com/problems/triangle/description/)

###### [借鉴](https://leetcode.com/problems/triangle/discuss/38735/Python-easy-to-understand-solutions-(top-down-bottom-up))

##### 最大子序和 [53](https://leetcode-cn.com/problems/maximum-subarray/)

##### 乘积最大子序列 [152](https://leetcode-cn.com/problems/maximum-product-subarray/description/)

##### 零钱兑换 [322](https://leetcode-cn.com/problems/coin-change/description/)
```go
// 递归

```

```go
// bfs

```

```go
// dp

```


##### 打家劫舍 [198](https://leetcode-cn.com/problems/house-robber/)

##### 打家劫舍 II [213](https://leetcode-cn.com/problems/house-robber-ii/description/)

##### 买卖股票的最佳时机 [121](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/#/description)

##### 买卖股票的最佳时机 II [122](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

##### 买卖股票的最佳时机 III [123](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)

##### 最佳买卖股票时机含冷冻期 [309](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

##### 买卖股票的最佳时机 IV [188](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/)

##### 买卖股票的最佳时机含手续费 [714](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

##### 买卖股票的最佳时机 [121](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/solution/yi-ge-fang-fa-tuan-mie-6-dao-gu-piao-wen-ti-by-l-3/)


#### 高级dp题目
##### 完全平方数 [279](https://leetcode-cn.com/problems/perfect-squares/)

##### 编辑距离（重点） [72](https://leetcode-cn.com/problems/edit-distance/)

##### 跳跃游戏 [55](https://leetcode-cn.com/problems/jump-game/)

##### 跳跃游戏 II [45](https://leetcode-cn.com/problems/jump-game-ii/)

##### 不同路径 [62](https://leetcode-cn.com/problems/unique-paths/)

##### 不同路径 II [63](https://leetcode-cn.com/problems/unique-paths-ii/)

##### 不同路径 III [980](https://leetcode-cn.com/problems/unique-paths-iii/)

##### 零钱兑换 [322](https://leetcode-cn.com/problems/coin-change/)

##### 零钱兑换 II [518](https://leetcode-cn.com/problems/coin-change-2/)

##### 最长有效括号 [32](https://leetcode-cn.com/problems/longest-valid-parentheses/)

##### 最小路径和 [64](https://leetcode-cn.com/problems/minimum-path-sum/)

##### 编辑距离 [72](https://leetcode-cn.com/problems/edit-distance/)

##### 解码方法 [91](https://leetcode-cn.com/problems/decode-ways/)

##### 最大正方形 [221](https://leetcode-cn.com/problems/maximal-square/)

##### 矩形区域不超过 K 的最大数值和 [363](https://leetcode-cn.com/problems/max-sum-of-rectangle-no-larger-than-k/)

##### 青蛙过河 [403](https://leetcode-cn.com/problems/frog-jump/)

##### 分割数组的最大值 [410](https://leetcode-cn.com/problems/split-array-largest-sum/)

##### 学生出勤记录 II [552](https://leetcode-cn.com/problems/student-attendance-record-ii/)

##### 任务调度器 [621](https://leetcode-cn.com/problems/task-scheduler/)

##### 回文子串 [647](https://leetcode-cn.com/problems/palindromic-substrings/)

##### 最小覆盖子串 [76](https://leetcode-cn.com/problems/minimum-window-substring/)

##### 戳气球 [321](https://leetcode-cn.com/problems/burst-balloons/)