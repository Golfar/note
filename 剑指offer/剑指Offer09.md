# 用两个栈实现队列

[232. 用栈实现队列 - 力扣（LeetCode）](https://leetcode.cn/problems/implement-queue-using-stacks/description/?utm_source=LCUS&utm_medium=ip_redirect&utm_campaign=transfer2china)

```java
class MyQueue {

    private Stack<Integer> s1, s2;

    public MyQueue() {
        s1 = new Stack<Integer>();
        s2 = new Stack<Integer>();
    }
    
    public void push(int x) {
        s1.push(x);
    }
    
    public int pop() {
        if(!s2.empty()) return s2.pop();
        while(!s1.empty()){
            s2.push(s1.pop());
        }
        return s2.pop();
    }
    
    public int peek() {
        if(!s2.empty()) return s2.peek();
        while(!s1.empty()){
            s2.push(s1.pop());
        }
        return s2.peek();
    }
    
    public boolean empty() {
        return s2.empty() && s1.empty();
    }
}
```

