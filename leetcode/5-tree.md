#### 二叉搜索树
也称二叉搜索排序树，二叉搜索树，有序二叉树，排序二叉树：
- 左子树上的所有节点的值均小于它的根节点的值
- 右子树上所有的节点的值都大于它的根节点的值
- 以此类推，左右子树也分别为二叉搜索树

##### 二叉树的中序遍历 [94](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
```go
func inorderTraversal(root *TreeNode) []int {
    res := make([]int, 0)
    inorder(root, &res)
    return res
}

func inorder(root *TreeNode, res *[]int) {
    if root != nil {
        inorder(root.Left, res)
        *res = append(*res, root.Val)
        inorder(root.Right, res)
    }
}
```
##### 二叉树的前序遍历 [144](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)
func preorderTraversal(root *TreeNode) []int {
    res := make([]int, 0)
    preOrder(root, &res)
    return res    
}

func preOrder(root *TreeNode, res *[]int) {
    if root != nil {
        *res = append(*res, root.Val)
        preOrder(root.Left, res)
        preOrder(root.Right, res)
    }
}

##### N叉树的后序遍历 [590](https://leetcode-cn.com/problems/n-ary-tree-postorder-traversal/)

##### N叉树的前序遍历 [589](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/)

##### N叉树的层序遍历 [429](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)