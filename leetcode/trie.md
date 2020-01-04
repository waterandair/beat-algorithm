##### Trie 模板
```python
class Trie(object):
  
	def __init__(self): 
		self.root = {} 
		self.end_of_word = "#" 
 
	def insert(self, word): 
		node = self.root 
		for char in word: 
			node = node.setdefault(char, {}) 
		node[self.end_of_word] = self.end_of_word 
 
	def search(self, word): 
		node = self.root 
		for char in word: 
			if char not in node: 
				return False 
			node = node[char] 
		return self.end_of_word in node 
 
	def startsWith(self, prefix): 
		node = self.root 
		for char in prefix: 
			if char not in node: 
				return False 
			node = node[char] 
		return True
```

##### 二叉树的层次遍历 [102](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)



##### 实现 Trie (前缀树) [208](https://leetcode-cn.com/problems/implement-trie-prefix-tree/solution/)


##### 单词搜索 II [212](https://leetcode-cn.com/problems/word-search-ii/)


