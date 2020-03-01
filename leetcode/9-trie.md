##### 实现 Trie (前缀树) [208](https://leetcode-cn.com/problems/implement-trie-prefix-tree/solution/)
```go
type Trie struct {
    End bool
    Ch [26]*Trie
}


/** Initialize your data structure here. */
func Constructor() Trie {
    var trie Trie
    return trie
}


/** Inserts a word into the trie. */
func (this *Trie) Insert(word string)  {
    cur := this
    for _, c := range word {
        idx := c - 'a'
        if cur.Ch[idx] == nil {
            var newnode Trie
            cur.Ch[idx] = &newnode
            cur = &newnode
        } else {
            cur = cur.Ch[idx]
        }
    }
    
    cur.End = true
}


/** Returns if the word is in the trie. */
func (this *Trie) Search(word string) bool {
    cur := this
    for _, c := range word {
        idx := c - 'a'
        fmt.Printf("%c,", c)
        if cur.Ch[idx] == nil {
            return false
        } else {
            cur = cur.Ch[idx]
        }
    }
    
    return cur.End
}


/** Returns if there is any word in the trie that starts with the given prefix. */
func (this *Trie) StartsWith(prefix string) bool {
    cur := this
    for _, c := range prefix {
        idx := c - 'a'
        if cur.Ch[idx] == nil {
            return false
        } else {
            cur = cur.Ch[idx]
        }
    }
    
    return true
}

```
##### 单词搜索 II [212](https://leetcode-cn.com/problems/word-search-ii/)
```go
func findWords(board [][]byte, words []string) []string {
	var results []string

	m := len(board)
	if m == 0 {
		return results
	}

	n := len(board[0])
	if n == 0 {
		return results
	}

	trie := buildTrie(words)

	for i := 0; i < m; i++ {
		for j := 0; j < n; j++ {
			dfs(board, i, j, trie, &results)
		}
	}

	return results
}

func dfs(board [][]byte, i int, j int, trie *TrieNode, results *[]string) {
	c := board[i][j]
	if c == '#' || trie.next[int(c-'a')] == nil {
		return
	}

	trie = trie.next[int(c-'a')]
	if len(trie.word) > 0 {
		// Found one
		*results = append(*results, trie.word)
		trie.word = ""
	}

	board[i][j] = '#'
	if i > 0 {
		dfs(board, i-1, j, trie, results)
	}

	if i < len(board)-1 {
		dfs(board, i+1, j, trie, results)
	}

	if j > 0 {
		dfs(board, i, j-1, trie, results)
	}

	if j < len(board[0])-1 {
		dfs(board, i, j+1, trie, results)
	}

	board[i][j] = c
}

type TrieNode struct {
	next [26]*TrieNode
	word string
}

func buildTrie(words []string) *TrieNode {
    root := new(TrieNode)
    for _, word := range words {
        cur := root
        for _, c := range word {
            idx := int(c-'a')
            if cur.next[idx] == nil {
                cur.next[idx] = new(TrieNode)
            }
            cur = cur.next[idx]
        }
        cur.word = word
    }

	return root
}
```


```go
type node map[string]node

func findWords(board [][]byte, words []string) []string {
	if len(words) == 0 || len(board) == 0 || len(board[0]) == 0 {
		return nil
	}

	trie := make(node)
	endOfWord := "#"

	for _, word := range words {
		root := trie
		for _, c := range word {
			if _, ok := root[string(c)]; !ok {
				root[string(c)] = make(node)
			}
			root = root[string(c)]
		}
		root[endOfWord] = make(node)
	}

	bx := []int{0, 0, -1, 1}
	by := []int{-1, 1, 0, 0}
	res := make(map[string]interface{})

	for y := 0; y < len(board); y++ {
		for x := 0; x < len(board[0]); x++ {
			dfs(board, x, y, "", bx, by, res, trie)
		}
	}

	result := make([]string, 0)
	for k, _ := range res {
		result = append(result, k)
	}

	return result
}

func dfs(board [][]byte, x, y int, word string, bx, by []int, res map[string]interface{}, trie map[string]node) {
	cur := board[y][x]
	if _, ok := trie[string(cur)]; !ok {
		return
	}

	word += string(cur)
	trie = trie[string(cur)]
	if _, ok := trie["#"]; ok {
		res[word] = nil
	}

	temp := board[y][x]
	board[y][x] = '@'

	for k := 0; k < 4; k++ {
		xi, yi := x+bx[k], y+by[k]
		if yi >= 0 && yi < len(board) && xi >= 0 && xi < len(board[0]) && board[yi][xi] != '@' {
			dfs(board, xi, yi, word, bx, by, res, trie)
		}
	}

	board[y][x] = temp
}

```


