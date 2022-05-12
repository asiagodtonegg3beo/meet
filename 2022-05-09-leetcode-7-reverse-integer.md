# 主題: 7. Reverse Integer
---
###### tags: `leetcode` `Medium`
##### 類型: `Math`


---
## 題目大要:
給定一個有號32bit整數x，回傳反轉後的數值。
如果反轉後的x超出有號32bit整數範圍[$-2^{31}$, $2^{31} - 1$]，則回傳 0。

Example 1:
```
Input: x = 123
Output: 321
```
Example 2:
```
Input: x = -123
Output: -321
```
Example 3:
```
Input: x = 120
Output: 21
```
Constraints:

$-2^{31}$ <= x <= $2^{31} - 1$



---
## 解法(演算法):
rev範圍:

$\begin{gathered}
-2^{31} \leq \text { rev } \cdot 10+\text { digit } \leq 2^{31}-1 \\ \\
\left\lceil\frac{-2^{31}}{10}\right\rceil \leq \text { rev } \leq\left\lfloor\frac{2^{31}-1}{10}\right\rfloor
\end{gathered}
$

INT_MIN / INT_MAX：變數類型為 int 的最小/大值，為巨集表示式

INT_MIN    = -2147483648 => $-2^{31}$
INT_MAX    = +2147483647 => $2^{31}-1$

```C++
digit:個位數字
rev:反轉數字，需介於2^31~2^31-1之間 => 使用long


while(x!=0){
    [-rev<2^31/10 or rev>(2^31-1)/10]
    if(rev<INT_MIN/10 || rev>INT_MAX/10)
        return 0;

    取個位數:
    digit = x % 10;

    不要個位數(取十位數字以上):
    x = x/10; (x/=10)


    新反轉數字 = 原反轉數字*10 + 個位數字
    rev = rev * 10 + digit;
}
return rev;

```
---
## 程式碼(C++)
官方解法：
* time complexity：$O(\log |x|)$，reverse的次數為十進制的位數。

* space complexity：$O(1)$。
```C++
class Solution {
public:

    int reverse(int x) {
        long result = 0; // 反轉後數值(rev)，[2^31~2^31-1]
        int num = 0;    // 個位數值(digit)
        while(x!=0){
            /* 反轉數字需介於(-2^31)/10~(+2^31)/10 之間，否則不處理 */
            if(result>INT_MAX/10 || result<INT_MIN/10)
                return 0;

            /* 取個位數 */
            num = x%10;

            /* 取完後丟棄個位數(/=10) */
            x /= 10;

            /* 反轉數字往前挪一位(*10)+個位數字 */
            result = result * 10 + num;
        }
        /* 回傳結果 */
        return result;
    }
};
```
簡潔寫法：
```C++
class Solution {
public:
int reverse(int x){
  	long n = 0;
  	while (x)
  	{
  		n = n * 10 + x % 10;
  		x /= 10;
  	}
  	return n > INT_MAX || n < INT_MIN ? 0 : n;
  }
}
```
