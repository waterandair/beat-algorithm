#### 数组
##### 移动 0
- https://leetcode-cn.com/problems/move-zeroes/
```go
func moveZeroes(nums []int)  {
    firstEero := 0
    for i := 0; i < len(nums); i ++ {
        if nums[i] != 0 {
            nums[firstEero] = nums[i]
            firstEero += 1
        }
    } 

    for i := firstEero; i<len(nums); i++ {
        nums[i] = 0
    }
}

func moveZeroes(nums []int)  {
   j := 0 
   for i := 0; i < len(nums); i ++ {
       if nums[i] != 0 {
           nums[j] = nums[i]
           if i != j {
               nums[i] = 0
           }
           j ++
       }
   }
}

```

##### 计算面积
https://leetcode-cn.com/problems/container-with-most-water/submissions/
```go
func maxArea(height []int) int {
	left := 0
	right := len(height) - 1
	max := -1
	for left < right {
		var area int
		if height[left] < height[right] {
			area = height[left] * (right - left)
			left++
		} else {
			area = height[right] * (right - left)
			right--
		}
		if area > max {
			max = area
		}
	}

	return max
}

```

##### 爬楼梯
https://leetcode-cn.com/problems/climbing-stairs/submissions/
```go
func climbStairs(n int) int {
    if n < 3 {
        return n
    }

    num := 0
    a := 1
    b := 2

    for n > 2 {
        num = a + b
        a = b
        b = num
        n -- 
    }

    return num
}
```
##### 两数之和
```go
func twoSum(nums []int, target int) []int {
	temp := make(map[int]int)
	length := len(nums)

	for i := 0; i < length; i ++ {
		temp[nums[i]] = i
	}

	for i:=0; i < length;i++ {
		t := target - nums[i]

		if j, ok := temp[t]; ok && j>i {
			return []int{i, j}
		}
	}

	return nil
}

func twoSum(nums []int, target int) []int {
    if len(nums) < 2 {
        return nil
    }

    temp := make(map[int]int)

    for i := 0; i < len(nums); i ++ {
        t := target - nums[i]
        if j, ok := temp[t]; ok {
            return []int{j, i}
        }

        temp[nums[i]] = i
    }

    return nil
}
```

##### 三数之和
暴力
```go

```
双指针
```go


```

##### 数组去重
```go
func removeDuplicates(nums []int) int {
    
    if len(nums) = 0 {
        return 0
    }
    
    left := 0 
    for i := 1; i < len(nums); i ++ {
        if nums[i] != nums[left] {
            left ++
            if i != left {
                nums[left] = nums[i]
            }
        }
    }

    return left + 1

}
```