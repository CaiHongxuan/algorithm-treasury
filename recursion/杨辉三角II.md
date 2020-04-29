# 杨辉三角 II

## 描述：

给定一个非负索引 k，其中 k ≤ 33，返回杨辉三角的第 k 行。

![杨辉三角](https://github.com/CaiHongxuan/algorithm-treasury/blob/master/images/PascalTriangleAnimated2.gif)

在杨辉三角中，每个数是它左上方和右上方的数的和。

示例:

> 输入: 3
> 输出: [1,3,3,1]

进阶：

你可以优化你的算法到 O(k) 空间复杂度吗？


## 分析：
1. 第 i 行的数据是由第 i-1 行的数据算出来的；
2. 第 i 行第 j 列的数： $result[$i][$j] = $result[$i - 1][$j - 1] + $result[$i - 1][$j]

由于要求算法要 O(k) 空间复杂度，所以在计算 i 行时必须在计算 i-1 行的结果数组上进行进一步计算。为了不影响每一行后续节点的计算值，可以考虑在第 i-1 行的结果数组前面插入0，此时，第 i 行第 j 列的数变为： $result[$i][$j] = $result[$i - 1][$j] + $result[$i - 1][$j + 1]
由于只需返回第 k 行，且是在同一个结果数组上计算，所以第 k 行的第 j 列的值为：
> $result[$j] = $result[$j] + $result[$j + 1]


## 解答：

```php
class Solution {

    /**
     * @param Integer $rowIndex
     * @return Integer[]
     */
    function getRow($rowIndex) {
        $result = [1];
        for ($i = 1; $i <= $rowIndex; $i++) {
            array_unshift($result, 0);
            for ($j = 0; $j <= $i; $j++) {
                $result[$j] = $result[$j] + $result[$j+1];
            }
        }
        return $result;
    }
}
```

来源：[力扣（LeetCode）](https://leetcode-cn.com/problems/pascals-triangle-ii)
链接：https://leetcode-cn.com/problems/pascals-triangle-ii
