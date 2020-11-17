找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

```

输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 

```

- 解法一 额外数组空间 C++
```C++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int size = nums.size();
        int res = 0;
        vector<int> num_record(size,0);
        for(int n: nums)
        {
            if(num_record[n]==1)
            {
                res = n;
                break;
            }
            num_record[n] = 1;
        }
        return res;
    }
};
```
- 解法二 set解法 C++
```C++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int size = nums.size();
        int res = 0;
        set<int>num_record;
        for(int n: nums)
        {
            if(num_record.count(n)!=0)
            {
                res = n;
                break;
            }
            num_record.insert(n);
        }
        return res;
    }
};
```
- 解法三 鸽巢原理 C++ 如果没有重复数字，那么正常排序后，数字i应该在下标为i的位置，所以思路是重头扫描数组，遇到下标为i的数字如果不是i的话，（假设为m),那么我们就拿与下标m的数字交换。在交换过程中，如果有重复的数字发生，那么终止返回ture


```C++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int size = nums.size();
        int res = 0;
        for(int i=0;i<size;i++)
        {
            while(nums[i] != i)
            {
                if(nums[i]==nums[nums[i]])
                {
                    res = nums[i];
                    break;
                }
                else
                {
                    int temp = nums[i];
                    nums[i] = nums[temp];
                    nums[temp] = temp;
                }
            }
        }
        return res;
    }
};
```
- 解法四 C++ 也可以用sort函数进行排序后，取相邻相同数返回