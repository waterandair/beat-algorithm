#### 分治模板 
```
def divide_conquer(problem, param1, param2, ...): 
  # recursion terminator 
  if problem is None: 
	print_result 
	return 

  # prepare data 
  data = prepare_data(problem) 
  subproblems = split_problem(problem, data) 

  # conquer subproblems 
  subresult1 = self.divide_conquer(subproblems[0], p1, ...) 
  subresult2 = self.divide_conquer(subproblems[1], p1, ...) 
  subresult3 = self.divide_conquer(subproblems[2], p1, ...) 
  …

  # process and generate the final result 
  result = process_result(subresult1, subresult2, subresult3, …)
	
  # revert the current level states
```

##### 括号生成 [22](https://leetcode-cn.com/problems/generate-parentheses/)

#####  Pow(x, n) [50](https://leetcode-cn.com/problems/powx-n/)

##### 子集 [78](https://leetcode-cn.com/problems/subsets/)

##### [牛顿迭代法原理](http://www.matrix67.com/blog/archives/361)

##### [牛顿迭代法代码](http://www.voidcn.com/article/p-eudisdmk-zm.html)

##### 多数元素 [169](https://leetcode-cn.com/problems/majority-element/description/)

##### 电话号码的字母组合 [17](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

##### N 皇后 [51](https://leetcode-cn.com/problems/n-queens/)