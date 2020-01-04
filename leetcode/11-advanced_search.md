#### 剪枝
##### 爬楼梯  [70](https://leetcode-cn.com/problems/climbing-stairs/)

##### 括号生成 [22](https://leetcode-cn.com/problems/generate-parentheses/)

##### N皇后 [51](https://leetcode-cn.com/problems/n-queens/)
###### N 皇后位运算代码示例
```python

	if n < 1: return [] 
	self.count = 0 
	self.DFS(n, 0, 0, 0, 0) 
	return self.count

def DFS(self, n, row, cols, pie, na): 
	# recursion terminator 
	if row >= n: 
		self.count += 1 
		return

	bits = (~(cols | pie | na)) & ((1 << n) — 1)  # 得到当前所有的空位

	while bits: 
		p = bits & —bits # 取到最低位的1
		bits = bits & (bits — 1) # 表示在p位置上放入皇后
		self.DFS(n, row + 1, cols | p, (pie | p) << 1, (na | p) >> 1) 
        # 不需要revert  cols, pie, na 的状态
```

```java
class Solution {
	private int size; 
	private int count;

	private void solve(int row, int ld, int rd) { 
		if (row == size) { 
			count++; 
			return; 
		}
		int pos = size & (~(row | ld | rd)); 
		while (pos != 0) { 
			int p = pos & (-pos); 
			pos -= p; // pos &= pos - 1; 
			solve(row | p, (ld | p) << 1, (rd | p) >> 1); 
		} 
	} 

public int totalNQueens(int n) { 
	count = 0; 
	size = (1 << n) - 1; 
	solve(0, 0, 0); 
	return count; 
  } 
}
```

非位运算判重（Python）
```
  def DFS(queens, xy_dif, xy_sum):
    p = len(queens)
    if p==n:
        result.append(queens)
        return None
    for q in range(n):
        if q not in queens and p-q not in xy_dif and \
          p+q not in xy_sum: 
            DFS(queens+[q], xy_dif+[p-q], xy_sum+[p+q])  
  result = []
  DFS([],[],[])
  return [ ["."*i + "Q" + "."*(n-i-1) for i in sol] for sol in result]
```
##### 有效的数独 [36](https://leetcode-cn.com/problems/valid-sudoku/description/)

##### 解数独 [37](https://leetcode-cn.com/problems/sudoku-solver/#/description)

#### 双向BFS的实现、特性和题解
##### 单词接龙 [127](https://leetcode-cn.com/problems/word-ladder/)

##### 最小基因变化 [433](https://leetcode-cn.com/problems/minimum-genetic-mutation/)

#### 启发式搜索
##### A*代码模板
```python
def AstarSearch(graph, start, end):

	pq = collections.priority_queue() # 优先级 —> 估价函数
	pq.append([start]) 
	visited.add(start)

	while pq: 
		node = pq.pop() # can we add more intelligence here ?
		visited.add(node)

		process(node) 
		nodes = generate_related_nodes(node) 
   unvisited = [node for node in nodes if node not in visited]
		pq.push(unvisited)
```

##### 二进制矩阵中的最短路径 [1091](https://leetcode-cn.com/problems/shortest-path-in-binary-matrix/)

##### 滑动谜题 [773](https://leetcode-cn.com/problems/sliding-puzzle/)

##### 解数独 [37](https://leetcode-cn.com/problems/sudoku-solver/#/description)