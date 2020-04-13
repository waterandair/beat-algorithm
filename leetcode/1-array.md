### 数组
#### 基础
##### 移动 0 [283](https://leetcode-cn.com/problems/move-zeroes/)
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
    lastNonZero := 0

    for i := 0; i < len(nums); i ++ {
        if nums[i] != 0 {
            if i == lastNonZero {
                lastNonZero ++
                continue
            }

            nums[lastNonZero] = nums[i]
            nums[i] = 0
            lastNonZero ++
        }
    } 
}

```



##### 计算面积 [11](https://leetcode-cn.com/problems/container-with-most-water/submissions/)

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

##### 爬楼梯 [70](https://leetcode-cn.com/problems/climbing-stairs/)
```go
func climbStairs(n int) int {
	if n < 4 {
		return n
	}

	num := 0
	a := 2
	b := 3
	for n > 3 {
		num = a + b
		a = b
		b = num
		n--
	}
	
	return num
}
```
##### 两数之和 [1](https://leetcode-cn.com/problems/two-sum/)
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

##### 三数之和 [15](https://leetcode-cn.com/problems/3sum/)
暴力
```go

```
双指针
```go

func threeSum(nums []int) [][]int {
    res := make([][]int, 0)
    if len(nums) < 3 {
        return res
    }
    sort.Ints(nums)

    for i:=0; i<len(nums)-2; i++ {
        if nums[i] > 0 {
            break;
        }

        l := i+1
        r := len(nums)-1

        for l < r {
            target := nums[i] + nums[l] + nums[r]
            switch {
                case target < 0 :
                    l++
                case target > 0 :
                    r -- 
                default:
                    res = append(res, []int{nums[i], nums[l], nums[r]})
                     for l < r && nums[l] == nums[l+1] {
                        l++
                    }

                    for l < r && nums[r] == nums[r-1] {
                        r--
                    }
                    l ++
                    r --
            }
        }

        for i < len(nums) - 2 && nums[i+1] == nums[i] {
            i++
        }
    }

    return res
}
```

##### 四数之和 [18](https://leetcode-cn.com/problems/4sum/)
##### N 数之和 


##### 数组去重 [26](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)
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

##### 旋转数组 [189](https://leetcode-cn.com/problems/rotate-array/)


##### 合并两个有序数组 [88](https://leetcode-cn.com/problems/merge-sorted-array/)
从后往前
```go
func merge(nums1 []int, m int, nums2 []int, n int)  {
    for n > 0 && m > 0 {
        if nums2[n-1] >= nums1[m-1] {
            nums1[m+n-1] = nums2[n-1]
            n --
            continue
        }

        nums1[m+n - 1] = nums1[m-1]
        m --
    }

    for i:=0; i<n ; i++ {
        nums1[i] = nums2[i]
    }
}
```

##### 加一 [66](https://leetcode-cn.com/problems/plus-one/)

