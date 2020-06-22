# 计算 x 的 n 次幂函数


## 描述：

实现 pow(x, n) ，即计算 x 的 n 次幂函数。


## 示例1：

> 输入: 2.00000, 10
> 输出: 1024.00000

## 示例2：

> 输入: 2.10000, 3
> 输出: 9.26100

## 示例3：

> 输入: 2.00000, -2
> 输出: 0.25000
> 解释: 2^-2 = 1/2^2 = 1/4 = 0.25


## 说明:

- -100.0 < x < 100.0
- n 是 32 位有符号整数，其数值范围是 [−2^31, 2^31 − 1] 。


## 解答：

### 法1（暴力法）：

```php
class Solution {

    /**
     * @param Float $x
     * @param Integer $n
     * @return Float
     */
    function myPow($x, $n) {
        $num = $n;
        if ($num < 0) {
            $x = 1 / $x;
            $num = -$num;
        }
        $result = 1;
        for ($i = 1; $i <= $num; $i++) {
            $result *= $x;
        }

        return $result;
    }
}
```

### 法2（迭代法）：

分析：暴力法是一个个计算，没有有效利用已经计算好的值。可以将已经计算出来的结果乘上其本身，如：x^n = x^(n/2) * x^(n/2)，对于n为奇数的情况，则只需再乘上x即可：x^n = x^((n-1)/2) * x^((n-1)/2) * x

```php
class Solution {

    /**
     * @param Float $x
     * @param Integer $n
     * @return Float
     */
    function myPow($x, $n) {
        $num = $n;
        if ($num < 0) {
            $x = 1 / $x;
            $num = -$num;
        }
        $result = 1;
        $current_product = $x;
        for ($i = $num; $i >= 1; $i /= 2) {
            if (($i % 2) == 1) {
                $result = $result * $current_product;
            }
            $current_product = $current_product * $current_product;
        }

        return $result;
    }
}
```

来源：[力扣（LeetCode）](https://leetcode-cn.com/explore/orignial/card/recursion-i/259/complexity-analysis/1227/)
链接：https://leetcode-cn.com/explore/orignial/card/recursion-i/259/complexity-analysis/1227/
