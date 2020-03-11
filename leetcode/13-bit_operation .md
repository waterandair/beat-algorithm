#### 位运算
左移 <<： 整体左移，末尾补0  
右移 >>： 整体右移，开头补0  
按位或 |： 两个二进制，同位同为1则输出1，否则输出0  
按位与 &： 两个二进制，同位同为0则输出0，否则输出1
按位取反 ~: 一个二进制，每一位取反  
按位异或 ^: 两个二进制，同位相同为0，不同为1  

##### XOR-异或的一些操作  

- x ^ 0 = x
- x ^ 1s(全1) = ~x 
- x ^ (~x) = 1s
- x ^ x = 0
- c = a^b => a^c=b, b^c=a
- a^b^c = a^(b^c) = (a^b)^c   

##### 指定位置的位运算常用操作
- 将 x 最右边的 n 为清零： x&(~0<<n)
- 获取 x 的第 n 位值(0 或者 1)： (x>>n)&1
- 获取 x 的第 n 位的幂值：x&(1<<(n-1)
- 仅将第 n 位置为 1： x|(1<<n)
- 仅将第 n 位置为 0： x&(~(1<<n))
- 将 x 最高位至第 n 位清零： x&((1<<n)-1)
- 将第 n 位至第 0 位清零： x&(~((1<<(n+1))-1)

##### 实践中位运算常见的操作  

- 判断奇偶: 偶 => (x&1)==1; 奇 => (x&1)==0  
- x/2 : x >> 1  
- 清零最低位的1： x&(x-1)
- 得到最低位的1： x&-x
- 0: x&~x
- 大写变小写、小写变大写 : 字符 ^= 32;
- 大写变小写、小写变小写 : 字符 |= 32;
- 小写变大写、大写变大写 : 字符 &= -33;



  



##### 位1的个数 [191](https://leetcode-cn.com/problems/number-of-1-bits/)
```go
func hammingWeight(num uint32) int {
    count := 0
    for num > 0 {
        count ++
        num = num & (num - 1)
    }

    return count
}
```
##### 2的幂 [231](https://leetcode-cn.com/problems/power-of-two/)
```go
func isPowerOfTwo(n int) bool {
    return n>0 && n&(n-1) == 0
}
```

##### 颠倒二进制位 [190](https://leetcode-cn.com/problems/reverse-bits/)
```go
func reverseBits(num uint32) uint32 {
    res := uint32(0)
    for i:=0; i<32; i++ {
        res += num & uint32(1) 
        num = num >> uint32(1)
        if i < 31 {
            res = res << uint32(1)
        }
    }

    return res
}
```
##### N皇后 [51](https://leetcode-cn.com/problems/n-queens/description/)

##### N皇后 II [52](https://leetcode-cn.com/problems/n-queens-ii/description/)

##### 比特位计数 [338](https://leetcode-cn.com/problems/counting-bits/description/)

