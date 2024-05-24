# 数组中的重复数字

[LCR 120. 寻找文件副本 - 力扣（LeetCode）](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

设备中存有 `n` 个文件，文件 `id` 记于数组 `documents`。若文件 `id` 相同，则定义为该文件存在副本。请返回任一存在副本的文件 `id`。

 

**示例 1：**

```
输入：documents = [2, 5, 3, 0, 5, 0]
输出：0 或 5
```

 

**提示：**

- `0 ≤ documents[i] ≤ n-1`
- `2 <= n <= 100000`

##  方法一：哈希

```java
class Solution {//用数组表示哈希
    public int findRepeatDocument(int[] documents) {
        int[] hash = new int[100000];
        for(int i : documents){
            if(hash[i] == 0){
                hash[i]++;
            }
            else{
                return i;
            }
        }
        return -1;
    }
}

class Solution {//使用HashSet
    public int findRepeatDocument(int[] documents) {
        HashSet hash = new HashSet();
        for(int i : documents){
            if(!hash.add(i)) return i;
        }
        return -1;
    }
}
```

## 方法二：原地交换

题目说明尚未被充分使用，即 在一个长度为 n 的数组 documents 里的所有数字都在 0 ~ n-1 的范围内 。 此说明含义：数组元素的 索引 和 值 是 一对多 的关系。
因此，可遍历数组并通过交换操作，使元素的 索引 与 值 一一对应（即 documents[i]=idocuments[i] = idocuments[i]=i ）。因而，就能通过索引映射对应的值，起到与字典等价的作用。

```java
class Solution {
    public int findRepeatDocument(int[] documents) {
        for(int i = 0; i < documents.length; ++i){
            if(documents[i] == i) continue;//注意这个if判断要在第二个if的前面。不然的话，已经在正确位置的数字会被认为是重复的
            if(documents[documents[i]] == documents[i]) {
                return documents[i];
            }
            int temp = documents[i];
            documents[i] = documents[temp];
            documents[temp] = temp;
            --i;//注意--，或者使用while
        }
        return -1;
    }
}
```

[287. 寻找重复数 - 力扣（LeetCode）](https://leetcode.cn/problems/find-the-duplicate-number/)

给定一个包含 `n + 1` 个整数的数组 `nums` ，其数字都在 `[1, n]` 范围内（包括 `1` 和 `n`），可知至少存在一个重复的整数。

假设 `nums` 只有 **一个重复的整数** ，返回 **这个重复的数** 。

你设计的解决方案必须 **不修改** 数组 `nums` 且只用常量级 `O(1)` 的额外空间。

 

**示例 1：**

```
输入：nums = [1,3,4,2,2]
输出：2
```

**示例 2：**

```
输入：nums = [3,1,3,4,2]
输出：3
```

**示例 3 :**

```
输入：nums = [3,3,3,3,3]
输出：3
```

 

 

**提示：**

- `1 <= n <= 105`
- `nums.length == n + 1`
- `1 <= nums[i] <= n`
- `nums` 中 **只有一个整数** 出现 **两次或多次** ，其余整数均只出现 **一次**

 

**进阶：**

- 如何证明 `nums` 中至少存在一个重复的数字?
- 你可以设计一个线性级时间复杂度 `O(n)` 的解决方案吗？

## 方法一：二分查找

```java
class Solution {//注意，这里的二分查找找的不是原数组nums，而是解空间数组[1,2,3,4,5,...,n]
    public int findDuplicate(int[] nums) {
        int l = 1, r = nums.length - 1, ans = -1;
        while(l <= r){
            int mid = (l + r) >> 1;
            int cnt = 0;
            for(int i = 0; i < nums.length; ++i){
                if(nums[i] <= mid){
                    cnt++;
                }
            }
            if(cnt <= mid){
                l = mid + 1;
            }else{
                r = mid - 1;
                ans = mid;
            }
        }
        return ans;
    }
}
```

我们首先计算`mid`，然后我们统计数组中小于等于`mid`元素的个数`k`，如果`k<=mid`的话，那么说明重复值在`[mid+1,n]`之间，否则的话重复值在`[1,mid]`之间。

```java
//1，3，4，2，2
```

我们此时的`mid=2`（也就是中间抽屉的位置），我们接着统计小于等于`2`的数的个数（统计抽屉左边元素个数），也就是`k=3`，而`3>2`，所以我们在`[1,2]`这个区间中找重复元素（抽屉左边找重复元素），再次计算`mid=1`，我们发现`k=1<=1`，此时我们就知道了`2`即为重复元素。

## 方法二：二进制

这个方法我们来将所有数二进制展开按位考虑如何找出重复的数，如果我们能确定重复数每一位是 111 还是 000 就可以按位还原出重复的数是什么。

考虑第`i`位，我们记 `nums`数组中二进制展开后第`i` 位为 `1` 的数有 `x` 个，数字 `[1,n]` 这 `n` 个数二进制展开后第 `i` 位为 `1` 的数有 `y` 个，那么重复的数第 `i` 位为 `1` 当且仅当 `x>y`。

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int n = nums.length, ans = 0;
        int bit_max = 31;
        while (((n - 1) >> bit_max) == 0) {//寻找最多多少位二进制
            bit_max -= 1;
        }
        for (int bit = 0; bit <= bit_max; ++bit) {
            int x = 0, y = 0;
            for (int i = 0; i < n; ++i) {//统计第bit位是否为1
                if ((nums[i] & (1 << bit)) != 0) {
                    x += 1;
                }
                if (i >= 1 && ((i & (1 << bit)) != 0)) {
                    y += 1;
                }
            }
            if (x > y) {//说明在bit位，重复数为1
                ans |= 1 << bit;
            }
        }
        return ans;
    }
}
```

## 方法三：环形链表

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = 0, fast = 0;
        do{
            slow = nums[slow];//向前走一步
            fast = nums[nums[fast]];//向前走两步
        }while(slow != fast)
        slow = 0;
        while(slow != fast){
            slow = nums[slow];
            fast = nums[fast];
        }
        return slow
    }
}
```

我们对 `nums` 数组建图，每个位置 `i` 连一条 `i→nums[i]` 的边。由于存在的重复的数字 `target`，因此 `target` 这个位置一定有起码两条指向它的边，因此整张图一定存在环，且我们要找到的 `target` 就是这个环的入口。

我们假设慢指针走了a步到达环的入口，又走了b步与快指针相遇。此时我们重置慢指针，两个指针每次都只走一步，最终相遇的地方一定是环的入口。

假设环长为L，最开始相遇时，慢指针走了a+b，快指针走了2a+2b。此时快指针比慢指针多走的a+b一定为整数倍的环长L。

此时我们将慢指针置为0，快指针不动，依然在环入口后b步的位置。此时慢指针走a步，快指针走了a+b步，慢指针到达入口，快指针同样走了k圈到达了入口。