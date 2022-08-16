# C++

## 贪心

### 分发饼干

假设你是一位很棒的家长，想要给你的孩子们一些小饼干。但是，每个孩子最多只能给一块饼干。

对每个孩子 i，都有一个胃口值 g[i]，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 j，都有一个尺寸 s[j] 。如果 s[j] >= g[i]，我们可以将这个饼干 j 分配给孩子 i ，这个孩子会得到满足。你的目标是尽可能满足越多数量的孩子，并输出这个最大数值。

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

例如， [1, 7, 4, 9, 2, 5] 是一个 摆动序列 ，因为差值 (6, -3, 5, -7, 3) 是正负交替出现的。

相反，[1, 4, 7, 2, 5] 和 [1, 7, 4, 5, 5] 不是摆动序列，第一个序列是因为它的前两个差值都是正数，第二个序列是因为它的最后一个差值为零。
子序列 可以通过从原始序列中删除一些（也可以不删除）元素来获得，剩下的元素保持其原始顺序。

给你一个整数数组 nums ，返回 nums 中作为 摆动序列 的 最长子序列的长度 。

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

子数组 是数组中的一个连续部分。

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/maximum-subarray/
链接：https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0053.%E6%9C%80%E5%A4%A7%E5%AD%90%E5%BA%8F%E5%92%8C.md

#### 解题思路
把从一开始的每一项加起来，
如果当前的和为负数的时候，则从零重新数

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

### 买卖股票的最佳时机II

给你一个整数数组 prices ，其中 prices[i] 表示某支股票第 i 天的价格。

在每一天，你可以决定是否购买和/或出售股票。你在任何时候 最多 只能持有 一股 股票。你也可以先购买，然后在 同一天 出售。

返回 你能获得的 最大 利润 。

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii
链接：https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0122.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BAII.md

#### 解题思路
如果某天的价格会低很则在前一天必会售出即是最优解，所以如果把前一天买的股票卖出去能赚钱的话则卖掉，把卖掉的钱加起来就是最大总利润

#### 代码

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int sum = 0;
        for (int i = 0; i < prices.size() - 1; i++) {
            if(sum < sum + (prices[i + 1] - prices[i])) {
                sum += (prices[i + 1] - prices[i]);
            }
        }
        return sum;
    }
};
```

### 跳跃游戏

给定一个非负整数数组 nums ，你最初位于数组的 第一个下标 。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个下标。

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/jump-game/
链接：https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0055.%E8%B7%B3%E8%B7%83%E6%B8%B8%E6%88%8F.md

#### 解题思路
在目前已知的范围内找到可以达到最大范围的点，即每个点可以到达的距离nums[i]加上那个点距离起始点的距离i，当可以达到的最大范围大于或等于数组的长度时就说明可以达到最后一个下标。

~~但是我竟然用了两个循环！！！因为完全不知道怎么写！！！耻辱啊耻辱啊！！！~~

#### 代码

```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int max = 0;
        int step = 0;
        for (int i = 0; i <= step; i++) {
            for (int j = 0; j < nums[i]; j++) {
                if (i + nums[i] > max) {
                    max = i + nums[i];
                }
            }
            step = max;
            if (step >= nums.size() - 1){
                return true;
            }
        }
        return false;
    }
};
```

#### 我老婆给我提供了一种全新的解,要比我自己的快很多

```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int max = 0;
        int step = 0;
        for (int i = 0; i <= step; i++) {
            for (int j = 0; j < nums[i]; j++) {
                if (i + nums[i] > max) {
                    max = i + nums[i];
                }
            }
            step = max;
            if (step >= nums.size() - 1){
                return true;
            }
        }
        return false;
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



