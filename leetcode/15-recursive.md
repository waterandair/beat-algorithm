首先找到最小问题的解，然后找到问题解决的过程

##### 递归数组求和
```go

```

##### 爬楼梯 [70](https://leetcode-cn.com/problems/climbing-stairs/)
```go
func groupAnagrams(n int) int {
	mem := make(map[int]int)

	return do(n, mem)
}

func do(n int, mem map[int]int) int {
	if n < 3 {
		return n
	}

	if mem[n] > 0 {
		return mem[n]
	}

	mem[n] = do(n-1, mem) + do(n-2, mem)
	return mem[n]
}

```

```go
func climbStairs(n int) int {
    if n < 3 {
        return n
    }

    num := 0
    a := 1
    b := 2

    for n > 2 {
        num = a + b
        a = b
        b = num
        n -- 
    }

    return num
}
```
##### 括号生成 [22](https://leetcode-cn.com/problems/generate-parentheses/)
```
func generateParenthesis(n int) []string {
    res := make([]string, 0)
    _gen(0,0,n,"",&res)
    return res
}

func _gen(left, right, n int, s string, res *[]string ) {
    if left == n && right == n {
        *res = append(*res, s)
        return  
    }

    if left < n {
        _gen(left + 1, right, n, s + "(", res)
    }

    if right < left {
        _gen(left, right + 1, n, s + ")", res)
    }
}
```

##### 翻转二叉树 [226](https://leetcode-cn.com/problems/invert-binary-tree/description/)

```go
func invertTree(root *TreeNode) *TreeNode {
    if root == nil {
		return nil
	}
	root.Left, root.Right = root.Right, root.Left
	invertTree(root.Left)
	invertTree(root.Right)
	return root
}
```
##### 验证二叉搜索树 [98](https://leetcode-cn.com/problems/validate-binary-search-tree/)
递归
```go

func isValidBST(root *TreeNode) bool {
    return helper(root, math.MinInt64, math.MaxInt64)
}

func helper(root *TreeNode, min, max int) bool {
    if root == nil {
        return true
    }
    if root.Val <= min || root.Val>=max {
        return false
    }

    return helper(root.Left, min, root.Val) && helper(root.Right, root.Val, max)
}
```

中序遍历/ 意外不能通过
```go
var last *TreeNode

func isValidBST(root *TreeNode) bool {
	last = &TreeNode{Val: -1 << 63}
	return dfs(root)
}

func dfs(root *TreeNode) bool {
	if root == nil {
		return true
	}
	if !dfs(root.Left) || root.Val <= last.Val {
		return false
	}
	last = root
	return dfs(root.Right)
}
```

##### 二叉树的最大深度 [104](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)
```go
func maxDepth(root *TreeNode) int {
	if root == nil {
		return 0
	}

	left := maxDepth(root.Left)
	right := maxDepth(root.Right)

	return int(math.Max(int64(left), int64(right)) + 1)
}
```

##### 二叉树的最小深度 [111](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)
```go
// 用例 [1,2] 不能通过
func minDepth(root *TreeNode) int {
	if root == nil {
		return 0
	}

	if root.Left == nil && root.Right == nil {
		return 1
	}

	left := minDepth(root.Left)
	right := minDepth(root.Right)

	return int(math.Min(float64(left), float64(right)) + 1)
}
```

```go
// 正确
func minDepth(root *TreeNode) int {
	if root == nil {
		return 0
	}

	if root.Left == nil {
		return minDepth(root.Right) + 1
	}
	if root.Right == nil {
		return minDepth(root.Left) + 1
	}

	return int(math.Min(float64(minDepth(root.Left)), float64(minDepth(root.Right))) + 1)
}
```

##### 二叉树的序列化与反序列化 [297](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)


##### 二叉树的最近公共祖先 [236](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

##### 从前序与中序遍历序列构造二叉树 [105](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

```
var preIndex int
func buildTree(preorder []int, inorder []int) *TreeNode {
    preIndex = 0
    length := len(preorder)
    if length == 0 || len(inorder) == 0 {
        return nil
    }

    inorderMap := make(map[int]int)
    for i, v := range inorder{
        inorderMap[v] = i
    }

    return helper(preorder,inorder, inorderMap, 0, length-1)

}

func helper(preorder []int,inorder []int, inorderMap map[int]int, start, end int)*TreeNode {
    if start > end {
        return nil
    }

    node := &TreeNode{
        Val: preorder[preIndex],
    }

    index := inorderMap[node.Val]
    preIndex ++

    node.Left = helper(preorder, inorder, inorderMap, start, index-1)
    node.Right = helper(preorder, inorder, inorderMap, index+1, end)

    return node
}
```
##### 从后序与中序遍历序列构造二叉树[106] 

```

```
##### 组合 [77](https://leetcode-cn.com/problems/combinations/)

##### 全排列 [46](https://leetcode-cn.com/problems/permutations/)

##### 全排列2 [47](https://leetcode-cn.com/problems/permutations-ii/)

