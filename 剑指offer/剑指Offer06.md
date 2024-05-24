# 从尾到头打印链表

[LCR 123. 图书整理 I - 力扣（LeetCode）](https://leetcode.cn/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

书店店员有一张链表形式的书单，每个节点代表一本书，节点中的值表示书的编号。为更方便整理书架，店员需要将书单倒过来排列，就可以从最后一本书开始整理，逐一将书放回到书架上。请倒序返回这个书单链表。

 

**示例 1：**

```
输入：head = [3,6,4,1]

输出：[1,4,6,3]
```

 

**提示：**

```
0 <= 链表长度 <= 10000
```

## 方法一：辅助栈

```java
class Solution {
    public int[] reverseBookList(ListNode head) {
        Stack<ListNode> s = new Stack<ListNode>();
        int length = 0;
        ListNode cur = head;
        while(cur != null){
            s.push(cur);
            cur = cur.next;
        }
        int[] res = new int[s.size()];
        int i = 0;
        while(!s.empty()){
            res[i++] = s.pop().val;
        }
        return res;
    }
}
```

## 方法二：递归

```java
class Solution {
    ArrayList<Integer> arr = new ArrayList<Integer>();
    public int[] reverseBookList(ListNode head) {
        digui(head);
        int[] res = new int[arr.size()];
        for(int i = 0; i < arr.size(); ++i){
            res[i] = arr.get(i);
        }
        return res;
    }
    private void digui(ListNode head){
        //if(head.next != null){如果输入为空，则不对
        //    digui(head.next);
        //}
        //arr.add(head.val);
        //return;
        if(head == null) return;
        digui(head.next);
        arr.add(head.val);
    }
}
```

