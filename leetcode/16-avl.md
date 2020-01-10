### AVL（平衡二叉树） 的性质
- 平衡因子在 [-1, 0, 1] 之间

### 红黑树（近似平衡二叉树）的性质
- 根节点时黑色的
- 每个叶子节点都是黑色的
- 不能有两个红色节点直接具有父子关系
- 从某个节点到它所有的叶子节点中的黑色节点的个数是相同的

**左右子树的高度差不超过两倍**

### AVL 和 红黑树的差别
- AVL 具有更好的查询速度，因为它是严格的平衡二叉树， 
- 红黑树， 具有更好的添加和删除操作，因为它是近似平衡二叉树，旋转操作做的比AVL少
- AVL 要存平衡因子和每个节点的高度，而红黑树只需要记录一个bit来存0/1，来表示红黑

读多写少用 avl， 其他情况用红黑树