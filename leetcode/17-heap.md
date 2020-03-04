##### 数据流中的第K大元素 [703](https://leetcode-cn.com/problems/kth-largest-element-in-a-stream/)
小顶堆

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


