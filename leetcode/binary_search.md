##### 二分查找模板
```
left, right = 0, len(array) - 1 
while left <= right: 
	  mid = (left + right) / 2 
	  if array[mid] == target: 
		    # find the target!! 
		    break or return result 
	  elif array[mid] < target: 
		    left = mid + 1 
	  else: 
		    right = mid - 1
```

##### x 的平方根 [69](https://leetcode-cn.com/problems/sqrtx/)

##### 有效的完全平方数 [367](https://leetcode-cn.com/problems/valid-perfect-square/)


##### 搜索旋转排序数组 [33](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

##### 搜索二维矩阵 [74](https://leetcode-cn.com/problems/search-a-2d-matrix/)

##### 寻找旋转排序数组中的最小值 [153](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)