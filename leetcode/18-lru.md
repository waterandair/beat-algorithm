##### lru 实现[146](https://leetcode-cn.com/problems/lru-cache/)

```golang
type LinkNode struct {
	key, val  int
	pre, next *LinkNode
}

type LRUCache struct {
	m          map[int]*LinkNode
	cap        int
	head, tail *LinkNode
}

func Constructor(capacity int) LRUCache {
	head := &LinkNode{0, 0, nil, nil}
	tail := &LinkNode{0, 0, nil, nil}
	head.next = tail
	tail.pre = head
	return LRUCache{make(map[int]*LinkNode), capacity, head, tail}
}

func (this *LRUCache) Get(key int) int {
	head := this.head
	cache := this.m
	if v, exist := cache[key]; exist {
		v.pre.next = v.next
		v.next.pre = v.pre
		v.next = head.next
		head.next.pre = v
		v.pre = head
		head.next = v
		return v.val
	} else {
		return -1
	}
}

func (this *LRUCache) Put(key int, value int) {
	head := this.head
	tail := this.tail
	cache := this.m
	//存在
	if v, exist := cache[key]; exist {
		//1.更新值
		v.val = value
		//2.移动到最前
		v.pre.next = v.next
		v.next.pre = v.pre
		v.next = head.next
		v.pre = head
		head.next.pre = v
		head.next = v
	} else {
		v := &LinkNode{key, value, nil, nil}
		if len(cache) == this.cap {
			//删除最后元素
			delete(cache, tail.pre.key)
			tail.pre.pre.next = tail
			tail.pre = tail.pre.pre
			//移动元素
			v.pre = head
			v.next = head.next
			v.next.pre = v
			head.next = v
			//放入map
			cache[key] = v
		} else {
			v.next = head.next
			v.pre = head
			head.next.pre = v
			head.next = v
			cache[key] = v
		}
	}
}
```