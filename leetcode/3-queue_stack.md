##### 有效的括号 [20](https://leetcode-cn.com/problems/valid-parentheses/)
```go
func isValid(s string) bool {
         
        right := map[string]string{")": "(", "]": "[", "}": "{"}
     
     	stack := []string{}
     
     	for _, str := range s {
     		if _, ok := right[string(str)]; ok {
     			if len(stack) == 0 || stack[len(stack)-1] != right[string(str)] {
     				return false
     			}
     			stack = stack[:len(stack)-1]
     		} else {
     			stack = append(stack, string(str))
     		}
     	}
     
     	if len(stack) != 0 {
     		return false
     	}
     
     	return true
}
```

```go
func isValid(s string) bool {
	m := map[rune]rune{'(': ')', '[': ']', '{': '}'}

	stack := make([]rune, 0)
	for _, v := range s {
		// right
		if m[v] == 0 {
			if len(stack) == 0 || m[stack[len(stack)-1]] != v {
				return false
			}
			stack = stack[:len(stack)-1]
			continue
		}

		// left
		stack = append(stack, v)
	}

	if len(stack) != 0 {
		return false
	}

	return true
}
```

##### 最小栈 [155](https://leetcode-cn.com/problems/min-stack/)
https://hansedong.github.io/2019/04/02/15/

```go
type MinStack struct {
	stackArray []int
	helpArray []int
}

/** initialize your data structure here. */
func Constructor() MinStack {
	minStack := MinStack{stackArray: make([]int, 0),helpArray:make([]int,0)}
	return minStack
}

func (this *MinStack) Push(x int) {
	this.stackArray = append(this.stackArray, x)
	if len(this.helpArray) == 0{
		this.helpArray = append(this.helpArray,x)
	}else if x <= this.helpArray[len(this.helpArray)-1]{
		this.helpArray = append(this.helpArray,x)
	}
}

func (this *MinStack) Pop() {
	if this.stackArray[len(this.stackArray)-1] == this.helpArray[len(this.helpArray)-1]{
		this.helpArray = this.helpArray[:len(this.helpArray)-1]
	}
	this.stackArray = this.stackArray[:len(this.stackArray)-1]

}

func (this *MinStack) Top() int {
	return this.stackArray[len(this.stackArray)-1]
}

func (this *MinStack) GetMin() int {

	return this.helpArray[len(this.helpArray)-1]
}
```

```go
type MinStack struct {
    next *MinStack
    element int
    minElement int
}

var head *MinStack


/** initialize your data structure here. */
func Constructor() MinStack {
    head = &MinStack{minElement:10000000000000,}
    return *head
    
}


func (this *MinStack) Push(x int)  {
    n := &MinStack{
        next:head,
        element:x,
        minElement:x,
    }
    if x > head.minElement {
        n.minElement = head.minElement
    }
    head = n
    
}


func (this *MinStack) Pop()  {
    head = head.next
}


func (this *MinStack) Top() int {
    return head.element
}


func (this *MinStack) GetMin() int {
    return head.minElement
    
}
```

##### 柱状图中最大的矩形 [84](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)
```go
// 暴力循环
func largestRectangleArea(heights []int) int {
	maxArea := 0
	for i := 0; i < len(heights); i++ {
		minHeight := heights[i]
		for j := i; j < len(heights); j++ {
			if heights[j] < minHeight {
				minHeight = heights[j]
			}

			area := minHeight * (j - i + 1)
			if area > maxArea {
				maxArea = area
			}
		}
	}

	return maxArea
}
```

```go
// 找左右边界
func largestRectangleArea(heights []int) int {
	maxArea := 0
	for i := 0; i < len(heights); i++ {
		left := i
		right := i + 1

		for left >= 0 && heights[left] >= heights[i] {
			left--
		}

		for right < len(heights) && heights[right] >= heights[i] {
			right++
		}

		area := heights[i] * (right - left - 1)
		if area > maxArea {
			maxArea = area
		}
	}

	return maxArea
}
```

```go
// 栈，原理还是通过找左右边界，栈中按升序，就可以依次找到左边界；进栈的时候判断是否小于栈顶元素就可以判断是否是右边界
func largestRectangleArea(heights []int) int {
	maxArea := 0
	stack := make([]int, 0)
	stack = append(stack, -1)

	for i, h := range heights {

		// 出栈
		for len(stack) != 1 && h <= heights[stack[len(stack)-1]] {
			height := heights[stack[len(stack)-1]]
			stack = stack[:len(stack)-1]
			area := height * (i - stack[len(stack)-1] - 1)
			if area > maxArea {
				maxArea = area
			}
		}

		stack = append(stack, i)
	}

	// 清空栈
	for len(stack) != 1 {
		height := heights[stack[len(stack)-1]]
		stack = stack[:len(stack)-1]

		area := height * (len(heights) - stack[len(stack)-1] - 1)
		if area > maxArea {
			maxArea = area
		}
	}

	return maxArea
}
```

##### 滑动窗口最大值 [239](https://leetcode-cn.com/problems/sliding-window-maximum/)
```go
// 堆
```
```go
// 双端队列
func maxSlidingWindow(nums []int, k int) []int {
	if len(nums) <= 1 || k <= 1 {
		return nums
	}
	res := make([]int, 0)
	dequeue := make([]int, 0)

	for i, num := range nums {
		if len(dequeue) != 0 && (i-dequeue[0]) == k {
			dequeue = dequeue[1:]
		}

		for len(dequeue) != 0 && num >= nums[dequeue[len(dequeue)-1]] {
			dequeue = dequeue[:len(dequeue)-1]
		}

		dequeue = append(dequeue, i)

		if i >= (k - 1) {
			res = append(res, nums[dequeue[0]])
		}
	}

	return res
}
```

#####  设计循环双端队列 [641](https://leetcode-cn.com/problems/design-circular-deque/)

##### 接雨水 [42](https://leetcode-cn.com/problems/trapping-rain-water/)

##### 用队列实现栈 [225](https://leetcode-cn.com/problems/implement-stack-using-queues/)

```go
type Queue struct {
	queue []int
}

type MyStack struct {
	queue *Queue
}

/** Initialize your data structure here. */
func Constructor() MyStack {
	return MyStack{queue: NewQueue()}
}

/** Push element x onto stack. */
func (this *MyStack) Push(x int) {
	this.queue.Push(x)
	for i := this.queue.Size() - 1; i > 0; i-- {
		this.queue.Push(this.queue.Pop())
	}
}

/** Removes the element on top of the stack and returns that element. */
func (this *MyStack) Pop() int {
	return this.queue.Pop()
}

/** Get the top element. */
func (this *MyStack) Top() int {
	return this.queue.Peek()
}

/** Returns whether the stack is empty. */
func (this *MyStack) Empty() bool {
	return this.queue.Size() == 0
}

func NewQueue() *Queue {
	return &Queue{queue: make([]int, 0)}
}

func (q *Queue) Push(i int) {
	q.queue = append(q.queue, i)
}

func (q *Queue) Pop() int {
	pop := q.queue[0]
	q.queue = q.queue[1:len(q.queue)]
	return pop
}

func (q *Queue) Peek() int {
	return q.queue[0]
}

func (q *Queue) Size() int {
	return len(q.queue)
}

/**
 * Your MyStack object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(x);
 * param_2 := obj.Pop();
 * param_3 := obj.Top();
 * param_4 := obj.Empty();
 */

```

##### 用栈实现队列 [232](https://leetcode-cn.com/problems/implement-queue-using-stacks/submissions/)
```go
type MyQueue struct {
	pushStack *Stack // 用于入队
	popStack  *Stack // 用于出队
}

/** Initialize your data structure here. */
func Constructor() MyQueue {
	return MyQueue{
		pushStack: NewStack(),
		popStack:  NewStack(),
	}
}

/** Push element x to the back of queue. */
func (this *MyQueue) Push(x int) {
	this.pushStack.Push(x)
}

/** Removes the element from in front of queue and returns that element. */
func (this *MyQueue) Pop() int {
	if this.popStack.Size() > 0 {
		return this.popStack.Pop()
	}

	for this.pushStack.Size() > 0 {
		this.popStack.Push(this.pushStack.Pop())
	}

	return this.popStack.Pop()
}

/** Get the front element. */
func (this *MyQueue) Peek() int {
	if this.popStack.Size() > 0 {
		return this.popStack.Peek()
	}

	for this.pushStack.Size() > 0 {
		this.popStack.Push(this.pushStack.Pop())
	}

	return this.popStack.Peek()
}

/** Returns whether the queue is empty. */
func (this *MyQueue) Empty() bool {
	return this.pushStack.Size() == 0 && this.popStack.Size() == 0
}

type Stack struct {
	stack []int
}

func NewStack() *Stack {
	return &Stack{stack: make([]int, 0)}
}

func (s *Stack) Push(x int) {
	s.stack = append(s.stack, x)
}

func (s *Stack) Peek() int {
	return s.stack[len(s.stack)-1]
}

func (s *Stack) Pop() int {
	pop := s.stack[len(s.stack)-1]
	s.stack = s.stack[0 : len(s.stack)-1]
	return pop
}

func (s *Stack) Size() int {
	return len(s.stack)
}
```