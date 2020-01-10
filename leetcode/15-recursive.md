首先找到最小问题的解，然后找到问题解决的过程

##### 递归数组求和
```go

```

##### 爬楼梯 [70](https://leetcode-cn.com/problems/climbing-stairs/)


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

##### 验证二叉搜索树 [98](https://leetcode-cn.com/problems/validate-binary-search-tree/)
递归
```go

```

中序遍历
```go

```

##### 二叉树的最大深度 [104](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)


##### 二叉树的最小深度 [111](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

##### 二叉树的序列化与反序列化 [297](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)


##### 二叉树的最近公共祖先 [236](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

##### 从前序与中序遍历序列构造二叉树 [105](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

##### 组合 [77](https://leetcode-cn.com/problems/combinations/)

##### 全排列 [46](https://leetcode-cn.com/problems/permutations/)

##### 全排列2 [47](https://leetcode-cn.com/problems/permutations-ii/)

