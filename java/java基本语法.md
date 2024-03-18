```java
//主类的名字必须和文件名相同，本文件名为Hello.java
public class Hello{
    
    //main方法必须为如下写法
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}
```

- 一个源文件中最多只能有一个`public`类，其他类的数量不受限制，且该类为主类，文件名必须和主类相同
- java文件编译时，每个类都会生成一个`.class`文件

```java
public class Plus{
    
    public static void main(String[] args){
        System.out.println(32 + 1);//33
        System.out.println(32 + "1");//321
        System.out.println(32 + 1 + "hello");//33hello
        System.out.println("hello" + 1 + 32);//hello132
    }
}
//加法运算中，从左向右计算，当有一项是字符串时，则作拼接运算
```



### 数据类型

Java数据类型主要分为两大类，分别是**基础数据类型和引用数据类型**

- 基础数据类型

  - 数值型

    - 整数类型

      byte[1]，short[2]，int[4]，long[8]

    - 浮点型

      float[4]，double[8]

  - 字符型

    char[2]

  - 布尔型

    boolean[1]

- 引用数据类型

  - 类
  - 接口
  - 数组

```java
public class Int{
    public static void main(String[] args){
        int a = 1;
        long b = 1L;
        long c = 1;
    }
}
```

- p42