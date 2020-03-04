#### 并查集
```go
type UnionFind struct {
	count    int
	unionSet []int
}

func NewUnionFind(n int) *UnionFind {
	u := new(UnionFind)
	u.count = n
	u.unionSet = make([]int, n)
	for i := 0; i < n; i++ {
		u.unionSet[i] = i
	}

	return u
}

func (u *UnionFind) Union(i, j int) {
	a := u.Find(i)
	b := u.Find(j)
	if a != b {
		u.unionSet[a] = b
		u.count--
	}
}

func (u *UnionFind) Find(i int) int {
	root := i
	for root != u.unionSet[root] {
		root = u.unionSet[u.unionSet[root]]
	}

	for i != u.unionSet[i] {
		x := i
		u.unionSet[x] = root
		i = u.unionSet[i]
	}

	return root
}

func (u *UnionFind) Count() int {
	return u.count
}
```
##### 岛屿数量 [200](https://leetcode-cn.com/problems/number-of-islands/)

##### 朋友圈 [547](https://leetcode-cn.com/problems/friend-circles/)
```go

func findCircleNum(M [][]int) int {
	if len(M) == 0 {
		return 0
	}

	unionFind := NewUnionFind(len(M))
	for i, m := range M {
		for j:= i+1; j < len(m); j++ {
			if i != j && M[i][j] == 1 {
				unionFind.Union(i, j)
			}
		}
	}

	return unionFind.Count()
}

```
##### 被围绕的区域 [130](https://leetcode-cn.com/problems/surrounded-regions/)

