##### 反转链表
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
##### 两两交换链表
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