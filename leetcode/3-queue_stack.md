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
```
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

```
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

##### 滑动窗口最大值 [239](https://leetcode-cn.com/problems/sliding-window-maximum/)
滑动窗口用队列

#####  设计循环双端队列 [641](https://leetcode-cn.com/problems/design-circular-deque/)

##### 接雨水 [42](https://leetcode-cn.com/problems/trapping-rain-water/)

##### 