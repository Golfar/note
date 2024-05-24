# 替换空格

[LCR 122. 路径加密 - 力扣（LeetCode）](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

假定一段路径记作字符串 `path`，其中以 "`.`" 作为分隔符。现需将路径加密，加密方法为将 `path` 中的分隔符替换为空格 "` `"，请返回加密后的字符串。

 

**示例 1：**

```
输入：path = "a.aef.qerf.bb"

输出："a aef qerf bb"
```

 

**限制：**

```
0 <= path.length <= 10000
```



```java
class Solution {
    public String pathEncryption(String path) {
        StringBuilder res = new StringBuilder();
        for(char c : path.toCharArray()){
            if(c != '.') res.append(c);
            else res.append(' ');
        }
        return res.toString();
    }
}

class Solution {
    public String pathEncryption(String path) {
        StringBuilder res = new StringBuilder();
        for(int i = 0; i < path.length(); ++i){
            char c = path.charAt(i);
            if(c != '.') res.append(c);
            else res.append(' ');
        }
        return res.toString();
    }
}

class Solution {
    public String pathEncryption(String path) {
        return path.replace(".", " ");
    }
}
```

