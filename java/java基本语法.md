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

![image-20240402155553888](./java基本语法.assets/image-20240402155553888.png)

### 逻辑运算符

![image-20240402155656142](./java基本语法.assets/image-20240402155656142.png)

- &&和&的区别

  &&：如果第一个条件为假，则不判断第二个条件，表达式整体为假

  &：如果第一个条件为假，仍会判断第二个条件

- ^为异或，相同为真，不同为假

### 赋值运算符

复合赋值运算符会进行类型转换

```java
public class Operator{
    public static void main(String[] args){
        byte b = 3;
        b += 3;//正确，等价于 b = (byte)(b + 3)
        b = b + 3;//报错，为int
    }
}
```

### 三元运算符

```java
//条件？表达式1：表达式2
public class Operator{
    public static void main(String[] args){
        int a = 3;
        int b = 4;
        int c = a > b ? a : b;//正确
        int c = a > b ? 1.1 : 3.4;//错误，double赋给int
    }
}
```

### Java标识符的命名规则和规范

- 包名

  多单词组成时，所有字母都小写，如aaa.bbb.ccc

- 类名、接口名

  所有单词的首字母大写，如TankShotGame，驼峰命名

- 变量名，方法名

  第一个单词首字母小写，后续单词的首字母大写tankShotGame

- 常量名

  所有字母大写，多个单词用下划线连接

### Java输入

```java
import java.util.Scanner;//注意有;

public class Input {
    public static void main(String[] args){
        //接受键盘输入
        Scanner myScanner = new Scanner(System.in);
        System.out.println("请输入名称");
        String name = myScanner.next();
        System.out.println("请输入年龄");
        int age = myScanner.nextInt();
        System.out.println(name + age);
    }

}
```

### 位运算

```java
public class Bit {
    public static void main(String[] args){
        int a = 1 >> 2;
        int c = 1 << 2;
        int a = 3 >>> 2;//逻辑右移，无符号右移，低位溢出，高位补0
    }
	//java中没有无符号数，所有数都有符号位
}
```

## 控制结构

```java
switch(){
    case 1:
        代码块;
        break;
    case 2:
        ...;
    default:
        
}
```

### break

```java
public static void main(String[] args){
        label1:
        for(int i = 0; i < 1000; ++i){
            label2:
            for(int j = 0; j < 1000; ++j){
                if (j==50){
                    System.out.println(i);
                    System.out.println(j);
                    break label1;

                }
            }
        }
    }
```

## 数组、排序和查找

### 数组

存放多个**同一类型**的数据。**数组也是一种数据类型，是引用类型**

```java
public class Array {
    public static void main(String[] args){
        double[] hens = {3, 5, 1, 3.4, 50};
        for(int i = 0; i < hens.length; ++i){
            //通过.length成员变量遍历数组，这是一个变量，不是方法。
        }
    }
}
```

通过.length成员变量遍历数组，**这是一个变量，不是方法。**

#### 数组初始化

```java
public class Array {
    public static void main(String[] args){
        double[] hens;
        double hen[];
        //上面两种方法等价
        
        int a[] = new int[5];//初始化一个大小为5的数组
        
        int a[];
        a = new int[10];
        //先声明，再初始化数组
        
        int a[] = {2, 3, 4, 5, 1};
        
        int a[] = new int[]{1,2,3,4};
    }
}
```

#### 数组赋值

```java
public class Array {
    public static void main(String[] args){
        //数组在默认情况下是引用传递，赋值的是地址
        int arr1[] = {1, 2, 3};
        int arr2[] = arr1;
        
        arr2[1] = 1;
        System.out.println(arr1[1]);//输出1
        
        int arr3 = new int[arr1.length];
        for(int i = 0; i < arr1.length; ++i){
            arr3[i] = arr1[i];
        }//这样完成数值拷贝
    }
}
```

![image-20240415131154639](./java基本语法.assets/image-20240415131154639.png)

#### 数组细节

- 数组默认值为0，布尔为`false`，字符串为`null`。
- 数组越界会抛出异常，但不会报错
- 数组是一个引用类型

#### 数组扩容

```java
public class Array {
    public static void main(String[] args){
        int arr[] = {1, 2, 3};
        int arrNew[] = new int[arr.length + 1];
        for (int i = 0; i < arr; ++i){
            arrNew[i] = arr[i];
        }
        arrNew[arrNew.length - 1] = 4;
        arr = arrNew;//原来的数组被jvm回收内存
    }
}
```

### 排序

```java
import java.util.Scanner;
//冒泡排序
public class Hello {
    public static void main(String[] args){
        Scanner myScanner = new Scanner(System.in);
        int[] data = new int[10];
        for(int i = 0; i < data.length; ++i){
            data[i] = myScanner.nextInt();
        }
        data = sort(data);
        for(int i = 0 ; i < data.length; ++i){
            System.out.println(data[i]);
        }
    }
    public static int[] sort(int[] data){
        for(int i = 0; i < data.length; ++i){
            for(int j = 0; j < data.length - i - 1; ++j){
                if(data[j] > data[j + 1]){
                    int temp = data[j];
                    data[j] = data[j + 1];
                    data[j + 1] = temp;
                }
            }
        }
        return data;
    }

}
```

### 二维数组

```java
public class Array {
    public static void main(String[] args){
        int[][] arr = {{1,2,3}, {1,2,3}};
        int[][] a = new int[2][3];
        
        //java中，允许二维数组的每个元素长度不一样
        int[][] b = new int[3][];
        for(int i = 0; i < b.length; ++i){
            b[i] = new int[i + 1];
        }
        
        
    }
}
```

![image-20240415134828705](./java基本语法.assets/image-20240415134828705.png)

# 面向对象方法

## 类与对象

```java
public class Array {
    public static void main(String[] args){
        Cat cat1 = new Cat();
        cat1.name = "小白";
        cat1.age = 3;
        cat2.color = "白色";
    }
}
class Cat{
    String name;
    int age;
    String color;
}
```

### 对象在内存中的存在形式

![image-20240415141842904](./java基本语法.assets/image-20240415141842904.png)

基本数据类型放在`堆区域`

![image-20240415142419942](./java基本语法.assets/image-20240415142419942.png)

-  栈：存放基本数据类型，局部变量
- 堆：存放对象
- 方法区：常量池（存放常量，如字符串等），类加载信息（属性信息和方法信息。只会在第一次声明类时加载，后续不用加载）

### 方法

```java
public class Object{
    public static void main(String[] args){
        Person p = new Person();
        p.speak();
    }
}

class Person{
    String name;
    int age;
    
    public void speak(){
        System.out.println("我是个好人");
        
    }
}
```

**方法中不能再定义方法**

- 同一个类中调用方法可以直接调用

  ```java
  class Person{
      String name;
      int age;
      
      public void speak(){
          System.out.println("我是个好人");
          
      }
      public void hi(){
          speak();
      }
  }
  ```

- 跨类要用对象调用

  ```java
  class Person{
      String name;
      int age;
      
      public void speak(){
          System.out.println("我是个好人");
          
      }
      public void hi(){
          speak();
      }
  }
  class Man{
      public void main(){
          speak();//报错
          Person p = new Person();
          p.speak();
      }
  }
  ```

- 局部基本变量是值传递
- 数组是引用传递
- 对象也是引用传递

### 重载

java中允许同一个类内多个同名方法存在，但要求形参列表不一致。对返回值无要求。

### 可变参数

java允许将同一个类中多个同名同功能但参数个数不同的方法，封装成一个方法。

```java
public static void main(String[] args){
    
}
class AddMethod{
    public int add(int... nums){
        //nums可以当作数组使用
        int res = 0;
        for(int i = 0; i < nums.length; ++i){
            res += nums[i];
        }
        return res;
    }
}
```

- 实参可以是0个或任意多个
- 实参可以为数组。。
- 可变参数的本质就是数组
- 可变参数可以和普通类型参数一起放在形参列表，但必须保证可变参数放在最后
- 一个形参列表中只能出现一个可变参数

- 局部变量必须赋值，它没有缺省值
- 全局变量可以不赋值，它有缺省值

### 构造器

```java
public static void main(String[] args){
    Person p = new Person("smith", 80);
}
class Person{
    String name;
    int age;
    
    public Person(String name, int age){
        //下面是错的，编译器不会自动调用this指针
        name = name;
        age = age;
        
        //应将形参名称和属性名称不同，或者使用this
        name = pName;
        this.age = age;
    }
}
```

- 构造器的修饰符只能是`public`或者默认
- 构造器没有返回值
- 方法名和类名相同
- 构造器的调用有编译器完成
- 构造方法可以重载
- 如果没有构造方法，编译器会自动生成一个缺省构造方法。
- 一旦自己定义了构造方法，缺省构造方法就会被覆盖。

对象的创建流程分析

1. 方法区加载类，*.class
2. 在堆中创建一个对象，值为默认值。
3. 根据构造方法初始化对象

### this

```java
class A{
    public A(){
        this(10,10);//r如果有这条语句，就必须是构造方法中的第一条语句。这条语句只能在构造器中使用。
        System.out.println("这是一个空构造器");
        
    }
    public A(int a, int b){
        System.out.println("这是一个含参构造器");
    }
}
```

## 包

- 区分相同名字的类
- 管理类
- 控制访问范围

包的基本语法：package com.myblog

package 打包

实质就是创建不同的文件夹来保存类

有点类似于`namespace`

### 包的命名

- 只能包含字母、数字、下划线
- 不能使用数字开头
- 不能使用保留字

### 命名规范

com.公司名.项目名.业务模块名

## 访问修饰符

- `public`，公开
- `protected`，对子类和同一个包中的类公开
- 默认，没有修饰符，向同一个包的类公开
- `private`，只有类本身能够访问
- ![image-20240416191412579](./java基本语法.assets/image-20240416191412579.png)
- 只有`public`和默认可以修饰类，访问规则同上
- 成员方法的访问规则也同上

## 面向对象的三大特征

**封装、继承、多态**

### 封装

把抽象出来的数据和对数据的操作封装在一起，数据被保护在内部，程序的其他部分只有通过被授权的操作才能对数据进行操作。

![image-20240416193623064](./java基本语法.assets/image-20240416193623064.png)

### 继承

提高代码复用性

![image-20240416195417267](./java基本语法.assets/image-20240416195417267.png)

- 私有属性不能在子类直接访问，需要通过`public`方法去访问
- 子类继承了所有的属性和方法，但是`private`修饰的属性和方法无法直接访问
- 当子类创建时，子类必须调用父类的构造器，完成父类的初始化
- 当创建子类对象时，不管使用子类哪个构造器，默认情况下都会调用父类的无参构造器，如果父类没有提供无参构造器，则必须在子类的构造器中用`super`去指定使用父类的哪个构造器去完成对父类的初始化工作。
- p290





