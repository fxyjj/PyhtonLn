# Some useful Method gained in Leetcode

## (2021/10/10) No.201: Bitwise AND of Numbers Range

```Given two integers left and right that represent the range [left, right], return the bitwise AND of all numbers in this range, inclusive.

Example 1:

Input: left = 5, right = 7
Output: 4

Example 2:

Input: left = 0, right = 0
Output: 0

Example 3:

Input: left = 1, right = 2147483647
Output: 0
```

* **Solution**:

由于范围内的数字连续，所以他们一定存在一个公共前缀使得 安位与过后可以保留下来，假设前i位相同，那么在[left,right] 范围的数字从小到大排序过后第 i+1 位到最后一位一定是00..0 -> 11..1, 那么问题就转换成了给定两个数字，秋他们的公共前缀，
```
def sol(left,right):
    shift = 0
    while left < right:
        left = left >> 1
        right = right >> 1
        shift += 1
    return left << shift
```

**基于Brian Kernighan 算法的位移**
这个算法的关键在于i每次对 num 和 num-1 安位与过后，num最右边的1会被抹去成0，所以我们也可以使用这种方法来寻找公共前缀。

```
def sol(left:int,right:int):
    while left < right:
        right = right & (right-1)
       return right

```