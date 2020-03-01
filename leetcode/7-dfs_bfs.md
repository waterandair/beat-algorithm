
##### 二叉树的层次遍历 [102](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/#/description)

BFS
```go
func levelOrder(root *TreeNode) [][]int {
    res := [][]int{}
    if root == nil {
        return res
    }
    
    queue := []*TreeNode{root}

    for len(queue)>0 {
        vals := []int{}
        nodes := []*TreeNode{}

        for _, node := range queue{
            vals = append(vals, node.Val)

            if node.Left != nil {
                nodes = append(nodes, node.Left)
            }

            if node.Right != nil {
                nodes = append(nodes, node.Right)
            }
        }

        queue = nodes
        res = append(res, vals)
    }


    return res
}
```

DFS
```go
func levelOrder(root *TreeNode) [][]int {
    res := [][]int{}
    helper(0, root, &res)
    return res
}

func helper(level int, node *TreeNode, res *[][]int) {
    if node == nil {
        return 
    }

    if len(*res) <= level {
        *res = append(*res, []int{})
    }

    (*res)[level] = append((*res)[level], node.Val)
    helper(level+1, node.Left, res)
    helper(level+1, node.Right, res)
}
```
##### 最小基因变化 [433](https://leetcode-cn.com/problems/minimum-genetic-mutation/#/description)

##### 括号生成 [22](https://leetcode-cn.com/problems/generate-parentheses/#/description)

##### 在每个树行中找最大值 [515](https://leetcode-cn.com/problems/find-largest-value-in-each-tree-row/#/description)

##### 单词接龙 [127](https://leetcode-cn.com/problems/word-ladder/description/)
```go
func ladderLength(beginWord string, endWord string, wordList []string) int {
	wordMap := make(map[string]bool)
	for _, s := range wordList {
		wordMap[s] = true
	}

	if !wordMap[endWord] {
		return 0
	}

	queue := []string{beginWord}
	step := 1

	for len(queue) > 0 {
		step++
		subQueue := make([]string, 0)

		for _, word := range queue {

			for i, w := range word {
				index := i
				for m := []byte("a")[0]; m <= []byte("z")[0]; m++ {
					if int32(m) == w {
						continue
					}

					tempWord := []byte(word)
					tempWord[index] = m

					if string(tempWord) == endWord {
						return step
					}

					if !wordMap[string(tempWord)] {
						continue
					}
					
					subQueue = append(subQueue, string(tempWord))
					delete(wordMap, string(tempWord))
					if len(wordMap) == 0 {
						return 0
					}
				}
			}
		}

		queue = subQueue
	}

	return 0
}
```

##### 单词接龙 II [126](https://leetcode-cn.com/problems/word-ladder-ii/description/)

##### 岛屿数量 [200](https://leetcode-cn.com/problems/number-of-islands/)

##### 扫雷游戏 [529](https://leetcode-cn.com/problems/minesweeper/description/)