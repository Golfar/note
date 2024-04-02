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



## 数据类型

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

public class Floatdetail{
    public static void main(String[] args){
        Float num1 = 1.1;//错误，小数默认为double类型
        Float num2 = 1.1f;//正确
        double num3 = 1.1;//正确
        double num4 = 1.1f;//正确
        double num5 = .512;//正确 num5  = 0.512。小数点前默认省略0
        double num6 = 5.12e2;//5.12*10^2。科学计数法
    }
}

public class FloatTrap{
    public static void main(String[] args){
        double num = 8.1 / 3;//num=2.6999999999
        
        if (num == 2.7){
            System.out.println("相等");//无输出
        }//应改为
        if (Math.abs(num - 2.7) < 0.00001){
            System.out.println("相等");
        }
    }
}

public class CharDetail{
    public static void main(String[] args){
        char ch1 = "a";//错误，双引号为字符串
        char ch2 = '\n';//转义字符
        //在java中，char的本质是一个整数，编码表为unicode
        System.out.println((int)ch1);//输出97
    }
}

public class BoolDetail{
    public static void main(String[] args){
        boolean flg = true;//取值仅能为true或false，不能为0或1
    }
}
```

编码表细节

- ASCII表

  1个字节

- Unicode

  字母和汉字都用2个字节表示

- utf-8

  大小可变的编码，字母用1个字节，汉字用3个字节

  对Unicode的一种改进

  使用1-6个字节表示一个符号

### 自动类型转换

精度小的类型可以自动转换成精度大的类型

![image-20240402135912111](./java基本语法.assets/image-20240402135912111.png)

- 多种数据类型运算时，系统会自动将其转换为容量最大的类型

  ```java
  public class ConvertDetail{
      public static void main(String[] args){
          double n = 1.1;
          float a = n + 1.1;//报错，右式为double类型
          float b = n + 1.1f;//正确
      }
  }
  ```

- byte和short不能和char之间相互自动转换

  ```java
  public class ConvertDetail{
      public static void main(String[] args){
          byte a = 10;//正确，在byte范围内能够赋值
          char ch1 = a;//错误
      }
  }
  ```

- byte，short，char可以进行运算，计算时会转换为int类型

  ```java
  public class ConvertDetail{
      public static void main(String[] args){
          byte a = 10;
          char ch1 = 97;
          short b = a + ch1;//报错，右式为int类型
      }
  }
  ```

- boolean不参与任何自动类型转换

### 强制类型转换

```java
public class ConvertDetail{
    public static void main(String[] args){
        int a = (int)1.9;//i = 1
        
        int b = (int)10 * 3.5 + 6 * 1.5;//报错，强转之对10有效
        int c = (int)(10 * 3.5 + 6 * 1.5);//正确
        
        int m = 100;
        char c = m;//报错
        char c = (char)m;
        
    }
}
```

![image-20240402141609662](./java基本语法.assets/image-20240402141609662.png)

### 字符串转换

```java
public class Basic2String{
    public static void main(String[] args){
        int a = 100;
        String s1 = a + "";//就能转换
        
        String s2 = "123";
        int b = Integer.parseInt(s2);
        double d = Double.parseDouble(s2);
        
        String s3 = "hello";
        int b = Integer.parseInt(s3);//不会报错，但会抛出异常
    }
}
```

## 运算符

### 算数运算符

![image-20240402142406919](./java基本语法.assets/image-20240402142406919.png)

```java
public class Operator{
    public static void main(String[] args){
        System.out.println(10 / 4);//输出2，而不是2.5
        double f = 10 / 4;//f=2.0
        
        double d = 5 / 9 * (256.4 - 100);//d=0，因为5/9会得0
    }
}
```

### 关系运算符

p69

