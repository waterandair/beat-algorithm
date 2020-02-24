##### 扩展阅读
- https://www.jianshu.com/p/b1ab4a170c3c
- https://leetcode-cn.com/problems/lru-cache/
- https://redisbook.readthedocs.io/en/latest/internal-datastruct/skiplist.html
- https://www.zhihu.com/question/20202931

##### 反转链表 [206](https://leetcode-cn.com/problems/reverse-linked-list/)
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseList(head *ListNode) *ListNode {
   if head == nil || head.Next == nil {
       return head
   }

    pre := reverseList(head.Next)

    head.Next.Next = head
    head.Next = nil
    return pre

}
```

```go
func reverseList(head *ListNode) *ListNode {
    var pre *ListNode

    for head != nil {
        next := head.Next

        head.Next = pre
        pre = head
        head = next
    }

    return pre
}
```
##### 两两交换链表 [24](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func swapPairs(head *ListNode) *ListNode {
   if head == nil || head.Next == nil {
       return head
   }

   next := head.Next
   head.Next = swapPairs(next.Next)
   next.Next = head

   return next
}

```

##### 203 删除链表中的元素
```go
func removeElements(head *ListNode, val int) *ListNode {
	for head != nil && head.Val == val {
		head = head.Next
	}

	if head == nil {
		return nil
	}

	list := head

	for head.Next != nil {
		if head.Next.Val == val {
			head.Next = head.Next.Next
		} else {
			head = head.Next
		}
	}

	return list
}

func remove(head *ListNode, val int) *ListNode {
	fakeHead := &ListNode{0, head}
	for p1, p2 := fakeHead, head; p2 != nil; {
		if p2.Val == val {
			p1.Next = p2.Next
			p2 = p2.Next
		} else {
			p1, p2 = p2, p2.Next
		}
	}
	return fakeHead.Next
}

func removeElements(head *ListNode, val int) *ListNode {
	fakeHead := &ListNode{0, head}
    fakeHead.Next = head

    head = fakeHead
	for head.Next != nil {
		if head.Next.Val == val {
			head.Next = head.Next.Next
		} else {
			head = head.Next
		}
	}

	return fakeHead.Next
}

```
递归
```go

```

##### 判断是否有环 [141](https://leetcode-cn.com/problems/linked-list-cycle/)


##### 环形链表2 [142](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

##### k 个一组进行翻转 [25](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)

##### 合并两个有序链表 [21](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

##### 其他

- 82
- reverse 
- 92
- 83
- 86
- 328
- 2
- 445
- 21
- 24 重要
- 25
- 147
- 148
- 237
- 19
- 61
- 143
- 234
