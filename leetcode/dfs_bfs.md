##### DFS
###### 递归写法
```go
visited = set() 

def dfs(node, visited):
    if node in visited: # terminator
    	# already visited 
    	return 

	visited.add(node) 

	# process current node here. 
	...
	for next_node in node.children(): 
		if next_node not in visited: 
			dfs(next_node, visited)
```



###### 非递归写法
```
def DFS(self, tree): 

	if tree.root is None: 
		return [] 

	visited, stack = [], [tree.root]

	while stack: 
		node = stack.pop() 
		visited.add(node)

		process (node) 
		nodes = generate_related_nodes(node) 
		stack.push(nodes) 

	# other processing work 
	...
```

##### BFS
```go
def BFS(graph, start, end):
    visited = set()
	queue = [] 
	queue.append([start]) 

	while queue: 
		node = queue.pop() 
		visited.add(node)

		process(node) 
		nodes = generate_related_nodes(node) 
		queue.push(nodes)

	# other processing work 
	...
```


##### 二叉树的层次遍历 [102](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/#/description)

##### 最小基因变化 [433](https://leetcode-cn.com/problems/minimum-genetic-mutation/#/description)

##### 括号生成 [22](https://leetcode-cn.com/problems/generate-parentheses/#/description)

##### 在每个树行中找最大值 [515](https://leetcode-cn.com/problems/find-largest-value-in-each-tree-row/#/description)

##### 单词接龙 [127](https://leetcode-cn.com/problems/word-ladder/description/)

##### 单词接龙 II [126](https://leetcode-cn.com/problems/word-ladder-ii/description/)

##### 岛屿数量 [200](https://leetcode-cn.com/problems/number-of-islands/)

##### 扫雷游戏 [529](https://leetcode-cn.com/problems/minesweeper/description/)