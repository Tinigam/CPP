# C++

## 贪心

### 分发饼干

对每个孩子 i，都有一个胃口值 g[i]，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 j，都有一个尺寸 s[j] 。如果 s[j] >= g[i]，我们可以将这个饼干 j 分配给孩子 i ，这个孩子会得到满足。你的目标是尽可能满足越多数量的孩子，并输出这个最大数值。

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/assign-cookies
链接：https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0455.%E5%88%86%E5%8F%91%E9%A5%BC%E5%B9%B2.md

#### 解题思路

先用小饼干喂饱小小孩

#### 代码

```cpp
 #include<algorithm>

class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
        int kid = 0;
        for (int i = 0; i < s.size(); i++) {
            if (kid < g.size() && g[kid] <= s[i]) {
                kid++;
            }
        }
        return kid;
    }
};
```

### 摆动序列

如果连续数字之间的差严格地在正数和负数之间交替，则数字序列称为 摆动序列 。第一个差（如果存在的话）可能是正数或负数。仅有一个元素或者含两个不等元素的序列也视作摆动序列。

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/wiggle-subsequence
链接：https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0376.%E6%91%86%E5%8A%A8%E5%BA%8F%E5%88%97.md

#### 解题思路
每次遇到和前一个差值相反的情况则result++并且储存差值

#### 代码

```cpp
class Solution {
public:
    int wiggleMaxLength(vector<int>& nums) {
        int max = 1;
        int dif1 = 0, dif2 = 0;
        for (int r = 0; r < nums.size() - 1; r++) {
            dif1 = nums[r + 1] - nums[r];
            cout<<dif1<<" "<<dif2<<endl;
            if ((dif1 > 0 && dif2 <= 0) || (dif1 < 0 && dif2 >= 0)) {
                max++;
                cout<<"max ="<<max<<endl;
                dif2 = dif1;
            }
        }
        return max;
    }
};
```

### 最大子序和

给你一个整数数组 nums ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

#### 解题思路
把从一开始的每一项加起来，
如果当前的和小于目前最大的和，则从零重新数

*初始当前最大值需要小于可能出现的最小值

#### 代码

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int max = -10000;
        int cur = 0;

        for (int i = 0; i < nums.size(); i++) {
            cur = cur + nums[i];
            if (cur > max) {
                max = cur;
            }
            if (cur < 0) {
                cur = 0;
            }
        }
        return max;
    }
};
```


## Function Example:

Sort:

```c++
int main()
{
    vector<int> v{ 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };
    sort(v.begin(), v.end(), greater<int>());
    return 0;
}
```



