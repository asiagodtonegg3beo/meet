# 主題: 11. Container With Most Water
---
###### tags: `leetcode` `Medium`
##### 類型:`Array` `Two Pointers` `Greedy`


---
## 題目大要
給定一個含有n個高度值(height)的整數陣列，N條垂直線繪製如下圖，使得第i條線是(i,0)和(i,height[i])。

找出兩條線與x軸表示成容器(Container)，使得這個容器裝滿最多水。

回傳此容器儲存水的最大容量

Example 1:

![](assets/markdown-img-paste-20220509212408328.png)

Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

---
## 解法(演算法):
```C++
//邊界,初始值:
l = 0;
u = height.size()-1;
area = 0 or INT_MIN;

//高度:取最小的高度(若取最大會溢出)
min(height[l],height[u]);

//不斷更新面積大小，找出最大面積
while(l<u){
    result = min(height[l],height[u])*(u-l);
    if(height[l]<height[u])
        l++;
    else
        u--;
    area = max(area,result);
}
return area;
```

---
## 程式碼(C++)
```C++
class Solution {
public:
    int maxArea(vector<int>& height) {
    int l = 0; //左牆index=0
    int u = height.size()-1; //右牆index=全長-1
    int area = 0; // 面積initial=0
    while(l<u){
        /* 水量=最小高度x寬度 */
        int result = min(height[l],height[u]) * (u-l);
        // 左邊的牆比右邊的牆高，寬度減1，index l++;
        if(height[l]<height[u]){
            l++;
        }
        // 右邊的牆比左邊的牆高，寬度減1，index u--;
        else{
            u--;
        }
        // 每一輪算最大面積
        area = max(area,result);
    }
    return area;
    }
};
```
