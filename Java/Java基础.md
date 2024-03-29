[toc]

# java

## 基础

1. 二进制
   1. ==十进制转换为二进制：除二取余，结果从下向上排列==
   2. ==二进制转换为十进制：从右到左依次序乘以位权==

2. 存储单元
   * 字节是我们常见计算机中最小存储单元，计算机存储的任何数据，都是以字节形式存储的
   * 8 bit (二进制位) 0000-0000表示为一个字节，1byte或者1B
   * ==8bit  =1B=1byte==、==1024B =1KB==、==1024KB=1MB==、==1024MB=1GB==、==1024GB=1T==

3. `JVM`
   * `java`虚拟机。所有的Java代码都运行在`jvm`上。
   * Java虚拟机本身不具有跨平台的功能，每个操作系统上都有不同版本的虚拟机

4. `JRE`和`JDK``
   * `jre：`Java运行时环境，包含`jvm`和运行时所需要的核心类库。
   * `jdk：`Java程序开发工具包。

5. Java开发程序的三个步骤
   * 编写源代码--->编译源程序--->运行
   * javac.exe编译器;Java.exe解释器

6. 注释
   * `//`单行注释
   * `/**/`多行注释

7. 关键字的概念与特征:完全小写的字母;在增强版的记事本，也就是开发工具中带颜色的字体

8. 标识符的概念与规则
   * 标识符：是指程序中，我们自己定义的类容
   * 命名规则: `硬性规则`
     * 包含`英文字母26个（区分大小写）`、`0-9`、`$(美元符号)`和`_(下划线)`。
     * 不能以数字开头
     * 不能是关键字 
   * 命名规则 `软性规则`
     * 类命名规范：首字母大写，后面每个单词首字母大写(大驼峰)
     * 变量命名规范：首字母小写，后面每个单词首字母大写(小驼峰)
     * 方法命名规范：同变量名
   
9. 四种权限修饰符:Java中有四种权限修饰符,能访问的权限。

   |              | public | > protected | > (default) 表示不写 | > private |
   | ------------ | ------ | ----------- | -------------------- | --------- |
   | 同一个类     | 能访问 | 能访问      | 能访问               | 能访问    |
   | 同一个包     | 能访问 | 能访问      | 能访问               | 不能访问  |
   | 不同包子类   | 能访问 | 能访问      | 不能访问             | 不能访问  |
   | 不同包非子类 | 能访问 | 不能访问    | 不能访问             | 不能访问  |

10. 基本类型与字符串之间的转换

   基本类型转换为String总共有三种方式

   ```java
   基本类型直接与””相连接即可;如:34+""
   Integer.toString(12)
   String.valueOf(12)
   ```

   String转换成对应的基本类型除了Character类之外,其他所有包装类都具有parseXxx静态方法可以将字符串参数转换为对应的基本类型:

   * `public static byte parseByte(String s)` :将字符串参数转换为对应的byte基本类型。
   * `public static short parseShort(String s)` :将字符串参数转换为对应的short基本类型。
   * `public static int parseInt(String s)` :将字符串参数转换为对应的int基本类型。
   * `public static long parseLong(String s)` :将字符串参数转换为对应的long基本类型。
   * `public static float parseFloat(String s)` :将字符串参数转换为对应的float基本类型。
   * `public static double parseDouble(String s)` :将字符串参数转换为对应的double基本类型。
   * `public static boolean parseBoolean (String s)` :将字符串参数转换为对应的boolean基本类型。

   ```java
   package baozhuanglei;
   
   public class Test02 {
       public static void main(String[] args) {
           //数据类型转换字符串
           int s = 12;
           String q = s+"";
           String w = Integer.toString(s);
           String e = String.valueOf(s);
           System.out.println(q+12+w+12+e+12);
           //字符串转换数据类型
           Integer str = Integer.parseInt("12");
           System.out.println(str+12);
       }
   }
   ```


### 常量的概念与分类

**常量**：在程序运行期间，固定不变的量

**分类**

| 类型       | 含义                                     | 数据举例                 |
| ---------- | ---------------------------------------- | ------------------------ |
| 整数常量   | 所有的整数                               | 0、1、2、3....           |
| 小数常量   | 所有小数                                 | 0.0、0.2、0.5            |
| 字符常量   | 单引号引起来、只能写一个字符、必须有内容 | 'a'、' '、'好'           |
| 字符串常量 | 双引号引起来、可以写多个字符、也可以不写 | "A"、"Hello"、"你好"、"" |
| 布尔常量   | 只有两个值                               | true、false              |
| 空常量     | 只有一个值                               | null                     |

**变量**：常量是固定不变的数据,那么在程序中可以变化的量称为变量。

> 数学中,可以使用字母代替数字运算,例如x=1+5或者6=x+5。
>
> 程序中,可以使用字母保存数字的方式进行运算,提高计算能力,可以解决更多的问题。比如x保存5,x也可以保存6,这样x保存的数据是可以改变的,也就是我们所讲解的变量。

Java中要求一个变量每次只能保存一个数据,必须要明确保存的数据类型。

### 数据类型

Java的数据类型分为两类：

* 基本数据类型：包括整数、浮点数、字符、布尔
* 引用数据类型：类、数组、接口

### 基本数据类型

四类八种基本数据类型

| 数据类型     | 关键宇       | 内存占用 | 取值范围              |
| ------------ | ------------ | -------- | --------------------- |
| 字节型       | byte         | 1个字节  | -128-127              |
| 短整型       | short        | 2个字节  | -32768-32767          |
| 整型         | int(默认)    | 4个字节  | -2^31^-2^31^-1        |
| 长整型       | long         | 8个字节  | -2^63^-2^63^-1        |
| 单精度浮点数 | float        | 4个字节  | 1.4013E-45-3.4028E+38 |
| 双精度浮点数 | double(默认) | 8个字节  | 4.9E-324-1.7977E+308  |
| 字符型       | char         | 2个字节  | 0-65535               |
| 布尔类型     | boolean      | 1个字节  | true,false            |

> Java中的默认类型:整数类型是int、浮点类型是double

1. 字符串不是基本类型,而是引用类型。
2. 浮点型可能只是一个近似值,并非精确的值。
3. 数据范围与字节数不一定相关,例如flpat数据范围比long更加广泛,但是float是4字节, long是8字节。
4. 浮点数当中默认类型是double。如果一定要使用float类型,需要加上一个后缀F。如果是整数,默认为int类型,如果一定要使用long类型,需要加上一个后缀L。推荐使用大写字母后缀。

### 方法

==方法其实就是若干语句的功能集合==

1. 修饰符:现阶段的固定写法,public static

2. 方法名称:方法的名字,规则和变量一样,小驼峰

3. 方法体:方法需要做的事情,若干行代码

4. 方法上有横线表示这个方法已经过时不用，有新的方法。

5. 参数：参数类型:进入方法的数据是什么类型；参数名称:进入方法的数据对应的变量名称 ；参数如果有多个`,`使用逗号进行分隔

   1. 有参数：小括号当中有内容,当一个方法需要一些数据条件,才能完成任务的时候,就是有参数。
   2. 无参数：小括号当中留空。一个方法不需要任何数据条件,自己就能独立完成任务,就是无参数。

6. 返回值：return:两个作用,第一停止当前方法,第二将后面的返回值还给调用处；返回值也就是方法执行后最终产生的数据结果；return后面的“返回值”,必须和方法名称前面的“返回值类型”,保持对应；返回值类型:也就是方法最终产生的数据结果是什么类型。

   1. 对于有返回值的方法,可以使用单独调用、打印调用或者赋值调用。

      ```mermaid
      graph LR
      subgraph 无返回值的方法
      A[调用方法]
      B[找到方法]
      C[传递参数]
      D[执行方法]
      E[将返回值交还给调用处]
      end
      B==>C==>D==>E==什么都不带==>A==>B
      ```

   2. 但是对于无返回值的方法,只能使用单独调用,不能使用打印调用或者赋值调用。

      ```mermaid
      graph LR
      subgraph 有返回值的方法
      AA[调用方法]
      BB[找到方法]
      CC[传递参数]
      DD[执行方法]
      EE[将返回值交还给调用处]
      AA==>BB==>CC==>DD==>EE==带着返回值==>AA
      end
      ```

```java
修饰符 返回值类型 方法名称(参数类型参数名称, ...){
      方法体
      return 返回值;
}
```

#### 方法的调用

1. 单独调用：`sum(10,20);`

   1. 返回值类型为==void==的，只能单独调用。

2. 打印调用：` System.out.println(sum(10,20));`

3. 赋值调用：`int number = sum(10,20);`

3. 快捷键：快速打印for如循环`参数.fori`

   ```java
   public class Demoe2MethodDefine {
       public static void main(String[] args) {
           //单独调用
           sum(10,20);
           //打印调用
           System.out.println(sum(10,20));
           //赋值调用
           int number = sum(10,20);
       }
       //方法
       public static  int sum(int a,int b){
           return a+b;
       }
   }
   ```
   

### 重载

==多个方法的名称一样,但是参数列表不一样。==

1. 方法重载（Overload）与下列因素相关: ==参数的个数、类型不同、多类型顺序不同==
2. 方法的重载（Overload）与下列因素无关:==与参数的名称、返回值类型无关==

```java
public class Demo01MethodOverload {
    public static void main(String[] args) {
        System.out.println(sum(10, 20));
        System.out.println(sum(10, 20, 30));
        System.out.println(sum(10, 20, 30, 40));
    }
    public static int sum(int a, int b) {
        return a + b;
    }
    public static int sum(int a, int b, int c) {
        return a + b + c;
    }
    public static int sum(int a, int b, int c, int d) {
        return a + b + c + d;
    }
}
```

### 数组

==是一种容器,可以同时存放多个数据值。==

1. 数组特点：==数组是一种引用数据类型，数组当中的多个数据,类型必须统一，数组的长度在程序运行期间不可改变==

2. 数组初始化：在内存当中创建一个数组,并且向其中赋予一些默认值。 

3. 两种常见的初始化方式:

   1. 动态初始化(指定长度):在创建数组的时候,直接指定数组当中的数据元素个数。

      ```java
      数据类型[] 数组名称 = new 数据类型[数组长度]
      * 左侧数据类型:也就是数组当中保存的数据,全都是统一的什么类型
      * 左侧的中括号:代表我是一个数组
      * 左侧数组名称:给数组取一个名字
      * 右侧的new:代表创建数组的动作
      * 右侧数据类型:必须和左边的数据类型保持一致
      * 右侧中括号的长度:也就是数组当中,到底可以保存多少个数据,是一个int数字
          int[] Array = new int[100]//100是长度
      ```

   2. 静态初始化(指定内容):在创建数组的时候,不直接指定数据个数多少,而是直接将具体的数据内容进行指定。

      ```java
      标准格式：
      数据类型[] 数组名称 = new 数据类型[]{元素1,元素2,..};
      省略格式：
      数据类型[] 数组名称 = {元素1,元素2,..};
      注意事项:
      1. 虽然静态初始化没有直接告诉长度,但是根据大括号里面的元素具体内容,也可以自动推算出来长度。
      2. 静态初始化标准格式可以拆分成为两个步骤。
      3. 动态初始化也可以拆分成为两个步骤。
      4. 静态初始化一旦使用省略格式,就不能拆分成为两个步骤了。
      //标准格式：
      int[] Array = new int[]{1,2,3,4,5,6,7}
      //省略格式
      int[] Array = {1,2,3,4,5,6,7}
      ```

   3. 使用建议：==如果不确定数组当中的具体内容,用动态初始化;否则,已经确定了具体的内容,用静态初始化。==

      * 直接打印数组名称：==得到的是数组对应的，内存地址哈希值。==
      * 访问数组元素的格式:`数组名称[索引值]`

      * 索引值:就是一个int数字,代表数组当中元素的编号；索引值从0开始,一直到“数组的长度-1"为止。

   4. 【注意】

      使用动态初始化数组的时候,其中的元素将会自动拥有一个默认值。规则如下:

      | 数据类型 | 默认值 |
      | -------- | ------ |
      | 整数类型 | e      |
      | 浮点类型 | 0.0    |
      | 字符类型 | lueeee |
      | 布尔类型 | false  |
      | 引用类型 | null   |

      注意事项:静态初始化其实也有默认值的过程,只不过系统自动马上将默认值替换成为了大括号当中的具体数值。

4. Java内存划分

5. Java的内存需要划分成为5个部分:

   1. 栈(Stack):存放的都是方法中的局部变量。方法的运行一定要在栈当中运行
      * 局部变量:方法的参数,或者是方法()内部的变量
      * 作用域:一旦超出作用域,立刻从栈内存当中消失。
   2. 堆(Heap):凡是new出来的东西,都在堆当中。
      * 堆内存里面的东西都有一个地址值:16进制
      * 堆内存里面的数据,都有默认值==同动态数组初始化后元素类型一致==。
   3. 方法区(Method Area):存储.class相关信息,包含方法的信息。
   4. 本地方法栈(Native Method Stack):与操作系统相关。
   5. 寄存器(pc Register):与CPU相关。

#### 数组工具类

1. Arrays

   `java.util.Arrays`是一个与数组相关的工具类,里面提供了大量静态方法,用来实现数组常见的操作。

   * `public static String tostring(数组)`:将参数数组变成字符串(按照默认格式: [元素1,元素2,元素3...])

   * `public static void sort(数组)`:按照默认升序(从小到大)对数组的元素进行排序。

   备注:

   1. 如果是数值, sort默认按照升序从小到大
   2. 如果是字符串, sort默认按照字母升序
   3. 如果是自定义的类型,那么这个自定义的类需要有Comparable或者Comparator接口的支持。

   ```java
   package xuexijava.jichu;
   
   import java.util.Arrays;
   
   public class ShuZhu {
       public static void main(String[] args) {
           int[] ints = {10,20,70,60,40,30};
           System.out.println(Arrays.toString(ints));
           Arrays.sort(ints);
           System.out.println(Arrays.toString(ints));
       }
   }
   ```

2. Math

   `java.util.Math`类是数学相关的工具类,里面提供了大量的静态方法,完成与数学运算相关的操作。

   * `blic static double abs(double num)`:获取绝对值。
   * `public static double ceil (double num)`:向上（向整方向）取整。
   * `public static double floor(double num)`:向下取整。
   * `public static long round(double num)`:四舍五入。

   ```java
   package xuexijava.jichu;
   
   public class Math01 {
       public static void main(String[] args) {
           double a = -1.0;
           //取绝对值,原来有几位后面就有几位
           System.out.println(Math.abs(a));
           //向上取整
           System.out.println(Math.ceil(5.1));
           //向下取整
           System.out.println(Math.floor(5.1));
           //四舍五入，不带小数点
           System.out.println(Math.round(5.1));
           System.out.println(Math.round(5.5));
       }
   }
   ```

## 面向对象

面向过程：当需要实现一个功能的时候,每一个具体的步骤都要亲力亲为,详细处理每一个细节。

面向对象：当需要实现一个功能的时候,不关心具体的步骤,而是找一个已经具有该功能的人,来帮我做事儿

```java
import java.util.Arrays;
public class Demo01PrintArray {
    public static void main(String[] args) {
        int[] array = {10, 20, 30, 40, 50};
        //面向过程
        System.out.print("[");
        for (int i = 0; i < array.length; i++) {
            if (i == array.length-1) {
                System.out.print(array[i] + "]");
            } else {
                System.out.print(array[i] + ",");
            }
        }
        //面向对象
        System.out.println(Arrays.toString(array));
    }
}
```

### 类的定义

1. 类由成员变量（属性）和成员方法（行为）构成

   1. 成员变量：`String name; // 姓名；int age; // 年龄`
   2. 成员方法：`public void eat() // 吃饭;public void sleep(); // 睡觉public void study() ;//学 习`

2. 对象的创建及使用

   1. 导包:也就是指出需要使用的类,在什么位置。

      * import 包名称.类名称;

      * 对于和当前类属于同一个包的情况,可以省略导包语句不写。

   2. 创建：格式:

      * 类名称对象名=new类名称();

   3. 使用,分为两种情况。

      * 使用成员变量:对象名.成员变量名
      * 使用成员方法:对象名,成员方法名(参数)
      * (也就是,想用谁,就用对象名点儿谁。)

   4. 注意事项：

      如果成员变量没有进行赋值,那么将会有一个默认值,规则和数组一样。 

3. 成员变量和局部变量区别

   1. 定义的位置不一样【重点】
      * 局部变量:在方法的内部
      * 成员变量:在方法的外部,直接写在类当中
   2. 作用范围不一样【重点】
      * 局部变量:只有方法当中才可以使用,出了方法就不能再用
      * 成员变量:整个类全都可以通用。
   3. 默认值不一样【重点】
      * 局部变量:没有默认值,如果要想使用,必须手动进行赋值
      * 成员变量:如果没有赋值,会有默认值,规则和数组一样
   4. 内存的位置不一样(了解)
      * 局部变量:位于栈内存
      * 成员变量:位于堆内存
   5. 生命周期不一样(了解)
      * 局部变量:随着方法进栈而诞生,随着方法出栈而消失
      * 成员变量:随着对象创建而诞生,随着对象被垃圾回收而消失
   6. 方法的参数是局部变量
      * 面向对象三大特征：继承，封装，多态

### 封装性

1. 方法本身就是一种封装

2. 关键字private也是一种封

   * 用private关键字将需要保护的成员变量进行修饰。一旦使用了==private==进行修饰,那么本类当中仍然可以随意访问。但是!超出了本类范围之外就不能再直接访问了。

   * 间接访问==private==成员变量,就是定义一对儿==Getter/Setter==方法

   * 必须叫==setXxx==或者是==getXxx==命名规则。

     * 对于Getter来说,不能有参数,返回值类型和成员变量对应;
     * 对于Setter来说,不能有返回值,参数类型和成员变量对应。 

   * 对于基本类型当中的boolean值, Getter方法一定要写成isxxx的形式,而setXxx规则不变。

     ```java
     package xuexijava.mainxiangduixing;
     public class Preson {
         private String name;
         private int age;
         public void show(){
             System.out.println(name + age);
         }
         public String getName() {
             return name;
         }
         public int getAge() {
             return age;
         }
         //传输数据
         public void setName(String name) {
             this.name = name;
         }
         //获取数据
         public void setAge(int age) {
             this.age = age;
         }
     }
     ```

     ```java
     package xuexijava.mainxiangduixing;
     
     public class Mode01 {
         public static void main(String[] args) {
             Preson preson = new Preson();
             preson.setName("哈哈");
             preson.setAge(20);
             preson.show();
         }
     }
     ```

### 构造方法

==构造方法是专门用来创建对象的方法,当我们通过关键字new来创建对象时,其实就是在调用构造方法。==

```java
//格式：
public 类名称(参数类型 参数名称) {
       方法体   
}
```

1. 注意事项：

   1. 构造方法的名称必须和所在的类名称完全一样,就连大小写也要一样
   2. 构造方法不要写返回值类型,连void都不写
   3. 构造方法不能return一个具体的返回值
   4. 如果没有编写任何构造方法,那么编译器将会默认赠送一个构造方法,没有参数
   5. 一旦编写了至少一个构造方法,那么编译器将不再赠送
   6. 构造方法也是可以进行重载的。

2. 标准类

   1. 一个标准的类通常要拥有下面四个组成部分（这样标准的类也叫做Java Bean）:

      1. 所有的成员变量都要使用private关键字修饰
      2. 为每一个成员变量编写一对儿Getter/Setter方法
      3. 编写一个无参数的构造方法
      4. 编写一个全参数的构造方法

      ```java
      package xuexijava.mainxiangduixing;
      
      public class Student {
          private String name;
          public int age;
      
          public Student() {
          }
      
          public Student(String name, int age) {
              this.name = name;
              this.age = age;
          }
      
          public String getName() {
              return name;
          }
      
          public void setName(String name) {
              this.name = name;
          }
      
          public int getAge() {
              return age;
          }
      
          public void setAge(int age) {
              this.age = age;
          }
      }
      //调用类
      class dome02{
          public static void main(String[] args) {
              Student stu1 = new Student();
              stu1.setName("啊哈");
              stu1.setAge(22);
              System.out.println(stu1.getName()+stu1.getAge());
              System.out.println("=================");
              Student stu2 = new Student("窝火",23);
              System.out.println(stu2.getName()+stu2.getAge());
              stu2.setAge(24);
              System.out.println("=================");
              System.out.println(stu2.getName()+stu2.getAge());
          }
      }
      ```

## API

1. Scanner：负责键盘输入
2. Random: 负责随机数生成
3. ArrayList: 集合用途跟数组差不多，比数组好用

### Scanner

==Scanner类的功能:可以实现键盘输入数据,到程序当中。==

引用类型的一般使用步骤;

1. 导包import 包路径.类名称;如果需要使用的目标类,和当前类位于同一个包下,则可以省略导包语句不写。
   * 只有java.Lang包下的内容不需要导包,其他的包都需要import语句。
2. 创建：
   * 类名称 对象名 = new 类名称();
3. 使用
   * 对象名,成员方法名() 

==system.in从键盘上输入==

获取键盘输入的一个int数字: int num = sc.nextInt();

获取键盘输入的一个字符串: String str = sc.next();

```java
package xuexijava.mainxiangduixing;

import java.util.Scanner;

public class dome03 {
    public static void main(String[] args) {
        //System.in表示重建盘输入
        Scanner sc = new Scanner(System.in);
        int num = sc.nextInt();
        System.out.println(num);
        String nbmp = sc.next();
        System.out.println(nbmp);
    }
}
```

### 匿名对象

匿名对象就是只有右边的对象,没有左边的名字和赋值运算符

`new 类名称();`

注意事项:匿名对象只能使用唯一的一次,下次再用不得不再创建一个新对象。

使用建议:如果确定有一个对象只需要使用唯一的一次,就可以用匿名对象。

```java
package xuexijava.mainxiangduixing;

public class Dome04 {
    String name;
    public void show(){
        System.out.println(name);
    }
}
class Dome05{
    public static void main(String[] args) {
        //匿名对象
        new Dome04().name = "哈哈哈";
    }
}
```

### Random

==Random类用来生成随机数字。==使用起来也是三个步骤:

1. 导包import java.util. Random;
2. 创建
   * Random r = new Random(); //小括号当中留空即可
3. 使用获取一个随机的int数字(范围是int所有范围,有正负两种): 
   * int num = r.nextInt()
4. 获取一个随机的int数字(参数代表了范围,左闭右开区间): 
   * int num = r.nextInt(3)实际上代表的含义是: [0,3),也就是0~2

```java
package xuexijava.mainxiangduixing;
//导包
import java.util.Random;

public class ModeRandom {
    public static void main(String[] args) {
        //创建
        Random random = new Random();
        //使用
        int r = random.nextInt();
        System.out.println(r);
    }
}
```

### ArrayList

==数组的长度不可以发生改变。但是Arraylist集合的长度是可以随意变化的。对于Arraylist来说,有一个尖括号`<E>`代表泛型。==

1. 泛型:也就是装在集合当中的所有元素,全都是统一的什么类型。

2. 注意:

   1. 泛型只能是引用类型,不能是基本类型。
   2. 创建了一个Arraylist集合,集合的名称是list,里面装的全都是String字符串类型的数据

3. 备注:从JDK 1.7+开始,右侧的尖括号内部可以不写内容,但是<>本身还是要写的。

4. 注意事项:对于Arraylist集合来说,直接打印得到的不是地址值,而是内容。如果内容是空,得到的是空的中括号: []

   ```java
   package xuexijava.caishuzi;
   
   import java.util.ArrayList;
   
   public class Mode01 {
       public static void main(String[] args) {
           ArrayList<String> list = new ArrayList<>();
           System.out.println(list);
           list.add("as");
           list.add("bs");
           list.add("cs");
           list.add("ds");
           System.out.println(list);
       }
   }
   ```

#### arraylist常用方法:

1. 向集合当中添加元素,参数的类型和泛型一致。返回值代表添加是否成功。

   ```java
   public boolean add(E e);
   //备注:对于ArrayList集合来说, add添加动作一定是成功的,所以返回值可用可不用。但是对于其他集合来说, add添加动作不一定成功。
   ```

2. 从集合当中获取元素,参数是索引编号,返回值就是对应位置的元素。

   ```java
   public E get(int index)
   ```

3. 从集合当中删除元素,参数是索引编号,返回值就是被删除掉的元素。

   ```java
   public E remove(int index)
   ```

4. 获取集合的尺寸长度,返回值是集合中包含的元素个数

   ```java
   public int size()
   ```

**例：**

```java
package xuexijava.caishuzi;

import java.util.ArrayList;

public class ArrayList01 {
    public static void main(String[] args){
        ArrayList<String> list = new ArrayList<>();
        System.out.println(list);
        //像集合中添加数据
        boolean success= list.add("哈哈哈");
        System.out.println(list);
        //查看添加动作是否成功
        System.out.println(success);

        list.add("哈哈哈");
        list.add("啊啊啊");
        list.add("黑猫警长");
        list.add("大耳贼");

        System.out.println(list);
        //返回对应位置的数据
        String name = list.get(2);
        System.out.println(name);
        //删除对应位置的数据
        String remo = list.remove(3);
        //查看删除的数据
        System.out.println(remo);
        //查看集合的长度
        int size = list.size();
        System.out.println(size);
    }
}
```

#### 向集合Arraylist当中存储基本类型数据

1. 必须使用基本类型对应的“包装类”。基本类型 包装类(引用类型,包装类都位于java.Lang包下)

2. 从JDK 1.5+开始,支持自动装箱、自动拆箱。

   * 自动装箱:基本类型-->包装类型
   * 自动拆箱:包装类型…>基本类型

3. | 基本数据类型 | 引用类            |
   | ------------ | ----------------- |
   | byte         | Byte              |
   | short        | Short             |
   | int          | Integer【特殊】   |
   | long         | Long              |
   | float        | Float             |
   | double       | Double            |
   | char         | Character【特殊】 |
   | boolean      | Boolean           |

4. 存储自定义对象

   ```java
   package xuexijava.caishuzi;
   
   import java.util.ArrayList;
   
   public class Student01 {
       public static void main(String[] args) {
           ArrayList<Student> list = new ArrayList<>();
           Student stu = new Student("哈哈",20);
           Student sta = new Student("嘿嘿",21);
           Student stb = new Student("丫丫",22);
           Student stc = new Student("呀呀",23);
   //        //set是重新赋值
   //        stu.setName("哈哈");
   //        Student a = stu.getName();
   //        list.add(a);
   //        stu.setAge(20);
   //        stu.setName("嘿嘿");
   //        stu.setAge(21);
   //        stu.setName("丫丫");
   //        stu.setAge(22);
           list.add(stu);
           list.add(sta);
           list.add(stb);
           list.add(stc);
   
           for (int i = 0; i < list.size(); i++) {
               Student a = list.get(i);
               System.out.println(a.getName()+a.getAge());
           }
       }
   }
   ```

## 字符串

### 字符串概述和特点

==程序当中所有的双引号字符串,都是String类的对象。(就算没有new,也照样是。)==

1. 字符串的特点;

   1. 字符串的内容永不可变。【重点】
   2. 正是因为字符串不可改变,所以字符串是可以共享使用的。
   3. 字符串效果上相当于是char[]字符数组,但是底层原理是byte[]字节数组。
   4. 字符串是常量，它们的值在创建之后不能更改。字符串缓冲区支持可变的字符串。因为String对象是不可变的,所以可以共享。

   ```java
   String str = "abc";
   等效于:
   char data[] = l'a', 'b', 'c'l;
   String str = new String (data);
   ```

2. 创建字符串构造方法和直接创建

   1. 构造方法
      1. `public String()`:创建一个空白字符串,不含有任何内容。
      2. `public String(char[] array)`:根据字符数组的内容,来创建对应的字符串。
      3. `public String(byte[] array)`:根据字节数组的内容,来创建对应的字符串。
   2. 直接创建
      1. `String str = "Hello"`注意:直接写上双引号,就是字符串对象。

   ```java
   package xuexijava.mainxiangduixing;
   
   public class String01 {
       public static void main(String[] args) {
           //使用空参构造
           String str1 = new String();//小括号留空,说明字符串什么内容都没有。
           System.out.println(str1);
   
           //根据字符数组创建字符串
           char[] charArray = {'a','b','c'};
           String str2 = new String(charArray);
           System.out.println(str2);
   
           //根据字节数组创建字符串
           byte[] byteArray = {97,98,99,100};
           String str3 = new String(byteArray);
           System.out.println(str3);
   
           //直接创建
           String str4 = "Hello";
           System.out.println(str4);
       }
   }
   ```

3. 字符串常量池

   1. 字符串常量池:程序当中直接写上的双引号字符串,就在字符串常量池中。

   2. `==`

      1. 对于基本类型来说,`==`是进行数值的比较。
      2. 对于引用类型来说,`==`是进行【地址值】的比较。
      3. 双引号直接写的字符串，在常量池中；new的不在常量池中

      ```java
      public static void main(String[] args){
          String str1 ="abc";
          String str2 ="abc";
          
          char[] charArray = {'a','b','c'};
          String str3 = new String(charArray);
          
          System.out.println(str1==str2);//true
          System.out.println(str1==str3);//flase
          System.out.println(str2==str3);//flase
      }
      ```

### 字符串相关方法

1. 比较方法

   ==`==`是进行对象的地址值比较,如果确实需要字符串的内容比较,可以使用两个方法:==

   1. `public boolean equals(Object obj):`参数可以是任何对象,只有参数是一个字符串并且内容相同的才会给true;否则返回false.

      1. 注意事项：
         1. 任何对象都能用Object进行接收。
         2. equals方法具有对称性,也就是a.equals(b)和b.equals(a)效果一样。
         3. 如果比较双方一个常量一个变量,推荐把常量字符串写在前面。
            * 推荐:` "abc".equals(str)` 不推荐:` str.equals("abc")`：报错控制指针错误

   2. `public boolean equalsIgnoreCase(String str)`:忽略大小写,进行内容比较。只有英文字母区分大小写。

      ```java
      package xuexijava.mainxiangduixing;
      
      public class String02 {
          public static void main(String[] args) {
              String str1 = "Hello";
              String str2 = "Hello";
              String str4 = "hello";
      
              char[] charArray = {'H','e','l','l','o'};
              String str3 = new String(charArray);
              System.out.println("Hello".equals(str1));
              System.out.println(str1.equals(str3));
      
              System.out.println(str1.equalsIgnoreCase(str4));
          }
      }
      ```

2. 获取方法

   1. `public int length()`:获取字符串当中含有的字符个数,拿到字符串长度。

   2. `public String concat(String str)`:将当前字符串和参数字符串拼接成为返回值新的字符串。

   3. `public char charAt(int index)`:获取指定索引位置的单个字符。(索引从0开始。)

   4. `public int indexof(String str)`:查找参数字符串在本字符串当中首次出现的索引位置,如果没有返回-1值。

      ```java
      package xuexijava.mainxiangduixing;
      
      public class String03 {
          public static void main(String[] args) {
              String str = "qwerty";
              //判断长度
              System.out.println(str.length());
              //拼接字符串
              String str1 = str.concat("qwe123rty");
              System.out.println(str1);
              //索引位置
              System.out.println(str1.charAt(6));
              //查看数字字符首次出现的位置
              System.out.println(str1.indexOf("er"));
              System.out.println(str1.indexOf("1"));
          }
      }
      ```

3. 截取方法

   1. `public String substring(int index)`:截取从参数位置一直到字符串末尾,返回新字符串。

   2. `public String substring(int begin, int end)`:截取从begin开始,一直到end结束,中间的字符串。

      * **备注**: [begin, end),包含左边,不包含右边。

      ```java
      System.out.println(str1.substring(6));
      System.out.println(str1.substring(6,7));
      ```

4. 转换方法

   1. `public char[] toCharArray()`:将当前字符串拆分成为字符数组作为返回值。

   2. `public byte[] getBytes()`:获得当前字符串底层的字节数组。

   3. `public String replace(CharSequence oldString, CharSequence newString)`:将所有出现的老字符串替换成为新的字符串,返回替换之后的结果新字符串。

      * **备注**: CharSequence意思就是说可以接受字符串类型。

      ```java
      char[] charArray = str1.toCharArray();
      System.out.println(charArray[0]);
      byte[] bytes = str1.getBytes();
      for (int i = 0; i < bytes.length; i++) {
          System.out.println(bytes[i]);
      }
      //替换
      System.out.println(str1.replace("123","456"));
      ```

5. 分割方法

   1. `public String[] split(String regex)`:按照参数的规则,将字符串切分成为若干部分。

   2. 注意事项:

      * split方法的参数其实是一个“正则表达式”,今后学习。今天要注意:如果按照英文句点“."进行切分,必须写`\\.`(两个反斜杠)

      ```java
      String str3 = "AAA,BBB,CCC";
      String str4 = "AAA.BBB.CCC";
      String[] charq = str3.split(",");
      for (int i = 0; i < charq.length; i++) {
          System.out.println(charq[i]);
      }
      String[] charw = str4.split("\\.");
      for (int i = 0; i < charw.length; i++) {
          System.out.println(charw[i]);
      }
      ```

## 静态关键字static

### static

==如果一个成员变量使用了static关键字,那么这个变量不再属于对象自己,而是属于所在的类。多个对象共享同一份数据==

1. static修饰方法

   1. 一旦使用static修饰成员方法,那么这就成为了静态方法。静态方法不属于对象,而是属于类的。

   2. 如果没有static关键字,那么必须首先创建对象,然后通过对象才能使用它。

   3. 如果有了static关键字,那么不需要创建对象,直接就能通过类名称来使用它。

   4. 无论是成员变量,还是成员方法。如果有了static,都推荐使用类名称进行调用。

      1. 静态变量:类名称.静态变量
      2. 静态方法:类名称.静态方法()
         * 对于本类中的静态方法，可以省略类名称

   5. 注意事项:

      1. 静态不能直接访问非静态。
         * 原因:因为在内存当中是【先】有的静态内容, 【后】有的非静态内容。==“先人不知道后人,但是后人知道先人。==
      2. 静态方法当中不能用this。原因: this代表当前对象,通过谁调用的方法,谁就是当前对象。

      ```java
      package xuexijava.jichu;
      
      public class MclassDiaoyong {
          public static void main(String[] args) {
              Mclass mclass = new Mclass();// 首先创建对象
              // 然后才能使用没有static关键字的内容
              mclass.fangFa();
              //对于静态方法来说,可以通过对象名进行调用,也可以直接通过类名称来调用。
              mclass.staticFangfa(); //正确,不推荐,这种写法在编译之后也会被javac翻译成为“类名称.静态方法名”
              Mclass.staticFangfa();// 正确,推
          }
      }
      ```

      ```java
      package xuexijava.jichu;
      
      public class Mclass {
          public void fangFa(){
              System.out.println("成员方法");
          }
          public static void staticFangfa(){
              System.out.println("静态方法");
          }
      }
      ```

2. 静态代码块

   1. 特点:当第一次用到本类时,静态代码块执行唯一的一次。

   2. 静态内容总是优先于非静态,所以静态代码块比构造方法先执行。

      1. 静态代码块的典型用途:==用来一次性地对静态成员变量进行赋值。==

      ```java
      static {
          //静态代码块的内容
      }
      ```

## 继承

==面向对象的三大特征:封装性、继承性、多态性。继承是多态的前提,如果没有继承,就没有多态。==

1. 继承主要解决的问题就是:==共性抽取。==

2. 继承关系当中的特点:

   1. 子类可以拥有父类的“内容”
   2. 子类还可以拥有自己专有的内容。

3. 格式：

   ```java
    定义父类的格式: (一个普通的类定义)
   public class 父类名称{
       //....
   }定义子类的格式:
   public class 类名 extends 父类名{
       //...
   }
   ```

   

### 继承中成员变量的访问特点

==在父子类的继承关系当中,如果成员变量重名,则创建子类对象时,访问有两种方式:==

1. 直接通过子类对象访问成员变量:
   * 等号左边是谁就优先用谁,没有则向上找。
2. 间接通过成员方法访问成员变量:
   * 该方法属于谁,就优先用谁，没有则向上找。
3. 区分子类中重名的三种变量
   * 局部变量:直接写成员变量名

   * 本类的成员变量:this.成员变量名

   * 父类的成员变量:super.成员变量名

4. 在父子类的继承关系当中,创建子类对象,访问成员方法的规则:
   * 创建的对象是谁,就优先用谁,如果没有则向上找。

5. 注意事项:无论是成员方法还是成员变量,如果没有都是向上找父类,绝对不会向下找子类的。

### 覆盖

重写(Override)概念:==在继承关系当中,方法的名称一样,参数列表也一样。==

* 覆盖(Override) :方法的名称一样,参数列表【也一样】。重写、覆写。
* 重载(Overload) :方法的名称一样,参数列表【不一样】

1. 方法的覆盖重写特点:==创建的是子类对象,则优先用子类方法。==

2. 方法覆盖重写的注意事项;

   1. 必须保证父子类之间方法的名称相同,参数列表也相同。
      * 写在方法前面,用来检测是不是有效的正确覆盖重写。安全保证
      * 这个注解就算不写,只要满足要求,也是正确的方法覆盖重写。
   2. 子类方法的返回值必须【小于等于】父类方法的返回值范围。
      * 提示: java.Lang.Object类是所有类的公共最高父类(祖宗类),java.Lang.String就是object的子类。
   3. 子类方法的权限必须【大于等于】父类方法的权限修饰符。
      * 小展提示: public > protected > (default) > private备注: (default)不是关键字default,而是什么都不写,留空。

3. 修饰符权限大小关系：public > protected > (default) > private

4. 设计原则:对于已经投入使用的类,尽量不要进行修改。推荐定义一个新的类,来重复利用其中共性内容，并且添加改动新内容。

5. 继承关系中,父子类构造方法的访问特点:

   1. 子类构造方法当中有一个默认隐含的"super()"调用,所以一定是先调用的父类构造,后执行的子类构造。
   2. 子类构造可以通过super关键字来调用父类重载构造。
   3. super的父类构造调用,必须是子类构造方法的第一个语句。不能一个子类构造调用多次super构造。

   ==总结:子类必须调用父类构造方法,不写则赠送super();写了则用写的指定的super调用, super只能有一个,还必须是第一个==

### super关键字

==super关键字用来访问父类内容==

1. 在子类的成员方法中,访问父类的成员变量。`super.成员变量名`
2. 在子类的成员方法中,访问父类的成员方法。`super.成员方法名`
3. 在子类的构造方法中,访问父类的构造方法。`super();`

### this关键字

当方法的局部变量和类的成员变量重名的时候,根据“就近原则”,优先使用局部变量；如果需要访问本类当中的成员变量,需要使用格式:this.成员变量名“；通过谁调用的方法,谁就是this

1. this.属性名
   * 大部分时候，普通方法访问其他方法、成员变量时无须使用 this 前缀，但如果方法里有个局部变量和成员变量同名，但程序又需要在该方法里访问这个被覆盖的成员变量，则必须使用 this 前缀。
2. this.方法名
   * this 关键字最大的作用就是让类中一个方法，访问该类里的另一个方法或实例变量。
3. this( ).访问构造方法
   * this( ) 用来访问本类的构造方法（构造方法是类的一种特殊方法，方法名称和类名相同，没有返回值。），括号中可以有参数，如果有参数就是调用指定的有参构造方法。
4. this关键字用来访问本类内容
   * 在本类的成员方法中,访问本类的成员变量。
   * 在本类的成员方法中,访问本类的另一个成员方法。
   * 在本类的构造方法中,访问本类的另一个构造方法。
   * 注意：在第三种用法当中要注意,this(...)调用也必须是构造方法的第一个语句。

### 抽象

* 抽象方法:就是加上abstract关键字,然后去掉大括号,直接分号结束。
* 抽象类:抽象方法所在的类,必须是抽象类才行。在class之前写上abstract即可。

```java
public abstract class Animal1T{
    //这是一个抽象方法,代表吃东西,但是具体是什么(大括号的内容)不确定。
    public abstract void eat();
    //这是普通的成员方法
    public void normalMethod();
}
```

**使用：**

1. 不能直接创建new抽象类对象。
2. 必须用一个子类来继承抽象父类。
3. 子类必须覆盖重写抽象父类当中所有的抽象方法。覆盖重写(实现) :子类去掉抽象方法的abstract表键字,然后补上方法体大括号。
4. 创建子类对象进行使用。
5. 抽象类不能创建对象,如果创建,编译无法通过而报错。只能创建其非抽象子类的对象。理解:假设创建了抽象类的对象,调用抽象的方法,而抽象方法没有具体的方法体,没有意义。
6. 抽象类中,可以有构造方法,是供子类创建对象时,初始化父类成员使用的。理解:子类的构造方法中,有默认的super(),需要访问父类构造方法。
7. 抽象类中,不一定包含抽象方法,但是有抽象方法的类必定是抽象类。理解:未包含抽象方法的抽象类,目的就是不想让调用者创建该类对象,通常用于某些特殊的类结构设t.
8. 抽象类的子类,必须重写抽象父类中所有的抽象方法,否则,编译无法通过而报错,除非该子类也是抽象类。理解:假设不重写所有抽象方法,则类中可能包含抽象方法,那么创建对象后,调用抽象的方法,没有意 

## 接口

==接口就是多个类的公共规范；接口是一种引用数据类型,最重要的内容就是其中的:抽象方法。==

如何定义一个接口的格式。`public interface 接口名称{//接口内容}`

```java
public interface 接口名称 {
}
```

备注:换成了关键字interface之后,编译生成的字节码文件仍然是: .java --> .class.

1. 如果是Java 7,那么接口中可以包含的内容有：常量、抽象方法
2. 如果是Java 8,还可以额外包含有：默认方法、静态方法
3. 如果是Java9,还可以额外包含有：私有方法 

### 定义接口的方法

使用接口的时候,需要注意

1. 接口是没有静态代码块或者构造方法的。
2. 一个类的直接父类是唯一的,但是一个类可以同时实现多个接口。
3. 格式：

```java
public class MyInterfaceImpl implements MyInterfaceA, MyInterfaceB{
    //覆盖重写所有抽象方法
}
```

3. 如果实现类所实现的多个接口当中,存在重复的抽象方法,那么只需要覆盖重写一次即可。

4. 如果实现类没有覆盖重写所有接口当中的所有抽象方法,那么实现类就必须是一个抽象类。

5. 如果实现类锁实现的多个接口当中,存在重复的默认方法,那么实现类一定要对冲突的默认方法进行覆盖重写。

6. 一个类如果直接父类当中的方法,和接口当中的默认方法产生了冲突,优先用父类当中的方法。

7. 类与类之间是单继承的。直接父类只有一个。

8. 类与接口之间是多实现的。一个类可以实现多个接口。

9. 接口与接口之间是多继承的。

   注意事项

   1. 多个父接口当中的抽象方法如果重复,没关系。
   2. 多个父接口当中的默认方法如果重复,弗么子接口必须进行默认方法的覆盖重写,【而且带着default关键字】。

#### 接口定义抽象方法和使用

在任何版本的Java中,接口都能定义抽象方法。

格式:`public abstract 返回值类型方法名称(参数列表);`

注意事项

1. 接口当中的抽象方法,修饰符必须是两个固定的关健字: public abstract
2. 这两个关键字修饰符,可以选择性地省略。(今天刚学,所以不推荐。)
3. 方法的三要素可以谁便定义

```java
public interface MyInterfaceAbs {
    //抽象方法
    public abstract void chouXiangFangFa();
    //抽象方法
    abstract void chouXiangFangFa1();
    //抽象方法
    void chouXiangFangFa2();
}
```

接口使用步骤;

1. 接口不能直接使用,必须有一个“实现类"来"实现”该接口。

   格式:

   `public class 实现类名称implements接口名称{}`

2. 接口的实现类必须覆盖重写(实现)接口中所有的抽象方法。现:去掉abstract关键字,加上方法体大括号。

3. 创建实现类的对象,进行使用。

```java
/*
*实现类，子类，
*/
public class Sxian  implements MyInterfaceAbs{
    public void chouXiangFangFa(){
        //方法体
    }
    
    public void chouXiangFangFa1(){
        //方法体
    }
    
    public void chouXiangFangFa2(){
        //方法体
    }
    
    public static void main(String[] args) {
        Sxian sxian = new Sxian();
        sian.chouXiangFangFa();
    }
}
```

#### 接口定义默认方法和使用

从Java 8开始,接口里允许定义默认方法。

格式:

`public default 返回值类型 方法名称(参数列表){方法体}`

备注:接口当中的默认方法,可以解决接口升级的问题。

默认方法会被实现类继承

1. 接口的默认方法,可以通过接口实现类对象,直接调用
2. 接口的默认方法,也可以被接口实现类进行覆盖重写。

```java
public default void  Abs(){
        //方法体
    }
```

#### 接口定义静态方法和使用

从Java 8开始

接口当中允许定义静态方法。

格式:

`public static 返回值类型方法名称(参数列表) {方法体}`

提示:就是将abstract或者default换成static即可,带上方法体。

注意:不能通过接口实现类的对象来调用接口当中的静态方法。

```java
public static void Asb(){
     //静态方法
    }
//调用
接口名称.Asb();
```

#### 接口定义私有方法和使用

问题描述:

我们需要抽取一个共有方法,用来解决两个默认方法之间重复代码的问题。但是这个共有方法不应该让实现类使用,应该是私有化的。

解决方案:从==Java 9==开始,接口当中允许定义私有方法。

1.普通私有方法,解决多个默认方法之间重复代码问题

格式:

`private返回值类型方法名称(参数列表) {方法体}`

2.静态私有方法,解决多个静态方法之间重复代码问题

`private static 返回值类型 方法名称(参数列表) {方法体}`

```java
package jiekou;

public interface Syff {
    public static void aSd(){
        System.out.println("静态方法1");
        rtq();
    }
    public static void sAd(){
        System.out.println("静态方法2");
        rtq();
    }

    public default void qWe(){
        System.out.println("默认方法1");
        rty();
    }
    public default void wQe(){
        System.out.println("默认方法2");
        rty();
    }
    //解决多个默认方法代码重复
    private void rty(){
        System.out.println("aaa");
        System.out.println("bbb");
        System.out.println("ccc");
    }
    //解决多个静态方法代码重复
    private static void rtq(){
        System.out.println("aaa");
        System.out.println("bbb");
        System.out.println("ccc");
    }
}
```

```java
package jiekou;

public class Syffimpl implements Syff{
    public static void main(String[] args) {
        Syffimpl syffimpl = new Syffimpl();
        syffimpl.qWe();
        syffimpl.wQe();
        Syff.aSd();
        Syff.sAd();
    }
}
```

#### 接口的常量定义和使用

接口当中也可以定义"成员变量”,但是必须使用public static final三个关键字进行修饰。

从效果上看,这其实就是接口的【常量】。

格式:

`public static final 数据类型 常量名称 = 数据值;`

备注:

一旦使用final关健字进行修饰,说明不可改变。

注意事项:

1. 接口当中的常量,可以省略public static final,注意:不写也照样是这样。
2. 接口当中的常量,必须进行赋值;不能不赋值。
3. 接口中常量的名称,使用完全大写的字母,用下划线进行分隔。(推荐命名规则)

```java
//定义
public static final int NUM_NUT=20;
//调用
接口名.常量名
```

## 多态

extends继承或者implements实现,是多态性的前提。

代码当中体现多态性,其实就是一句话:父类引用指向子类对象。

`父类名 对象名 = new 子类名();`或者`接口名 对象名 = new 实现类名();`

```java
//父类
public class Fu {
    public void show(){
        System.out.println("父类方法");
    }
    public void showe(){
        System.out.println("父类特有方法");
    }
}
//子类
public class Zi extends Fu{
    @Override
    public void show() {
        System.out.println("子类方法");
    }
}
//实现类
public class DuoTai {
    public static void main(String[] args) {
        Fu obj = new Zi();
        obj.show();
        obj.showe();
    }
}
```

1. 多态中成员变量的使用特点
   1. 直接通过对象名称访问成员变量：看等号左边是谁,优先用谁,没有则向上找，成员变量不能进行覆盖重写
   2. 间接通过成员方法访问成员变量：看该方法属于谁,优先用谁,没有则向上找。
2. 在多态的代码当中,成员方法的访问规则是:看new的是谁,就优先用谁,没有则向上找。
   1. 成员变量:编译看左边,运行还看左边。
   2. 成员方法:编译看左边,运行看右边。

==使用多态的好处：类型不会改变==

### 对象向上转型

1. 对象的向上转型,其实就是多态写法:对象一旦向上转型为父类,那么就无法调用子原本特有的内容。
   1. 格式:`父类名称对象名=new子类名称()`:
   2. 含义:右侧创建一个子类对象,把它当做父类来看待使用。
   3. 注意事项:==向上转型一定是安全的。==从小范围转向了大范围,

==类似于:double num = 100; //正确, int --> double, 自动类型转==

```java
//父类
public class Fu {
    public void show(){
        System.out.println("父类方法");
    }
}
//子类
public class Zi extends Fu{
    @Override
    public void show() {
        System.out.println("子类方法");
    }
    public void showe(){
        System.out.println("父类特有方法");
    }
}
//实现类
public class DuoTai {
    public static void main(String[] args) {
        Fu obj = new Zi();
        obj.show();
    }
}
```

### 对象向下转型

1. 对象的向下转型,其实是一个【还原】的动作。
   1. 格式:`子类名称 对象名 = (子类名称)父类对象:`
   2. 含义:将父类对象,【还原】成为本来的子类对象。

==`类似于:int num = (int) 10.0: // 可以int num = (int) 10.5;//不可以,精度损失`;ClassCastException:类转换异常==

```java
//父类
public class Fu {
    public void show(){
        System.out.println("父类方法");
    }
}
//子类
public class Zi extends Fu{
    @Override
    public void show() {
        System.out.println("子类方法");
    }
    public void showe(){
        System.out.println("父类特有方法");
    }
}
//实现类
public class DuoTai {
    public static void main(String[] args) {
        Fu obj = new Zi();
        obj.show();
        Zi one = (zi)obj;
        one.showe();
    }
}
```

### instanceof关键字

如何才能知道一个父类引用的对象,本来是什么子类?

格式:`对象名 instanceof 类名称`

这将会得到一个boolean值结果,也就是判断前面的对象能不能当做后面类型的实例。

```java
对象名 instanceof 子类名//结果为真或假（true/false）
```

### final关键字

最终的不可变的

常见四种用法：可以用来修饰一个类;可以用来修饰一个方法;还可以用来修饰一个局部变量;还可以用来修饰一个成员变量

1. 用于修饰类
   1. 当final关键字用来修饰一个类的时候
   2. 格式:`public final class 名称(){}`
   3. 含义:当前这个类不能有任何的子类。

==一个类如果是final的,那么其中所有的成员方法都无法进行覆盖重写==

2. 用于修饰一个成员方法
   1. 当final关键字用来修饰一个方法的时候,这个方法就是最终方法,也就是不能被覆盖重写。
   2. 格式:`修饰符 final 返回值类型 方法名称(参数列表) {//方法体}`

==对于类、方法来说, abstract关键字和final关键字不能同时使用,因为矛盾。==

* **abstract:**抽象表示一定要覆盖重写

* **final:**表示不能被覆盖重写

3. 用于修饰局部变量

==一旦使用final用来修饰局部变量,那么这个变量就不能进行更改:“一次赋值,终生不变”==

*  **对于基本类型来说**,不可变说的是变量当中的数据不可改变对

*  **对于引用类型来说**,不可变说的是变量当中的地址值不可改变

4. 用于修饰成员变量

==对于成员变量来说,如果使用final关键字修饰,那么这个变量也照样是不可变。==

1. 由于成员变量具有默认值,所以用了final之后必须手动赋值,不会再给默认值了。
2. 对于final的成员变量,要么使用直接赋值,要么通过构造方法赋值。二者选其一。
3. 必须保证类当中所有重载的构造方法,都最终会对final的成员变量进行赋值。

## 内部类

果一个事物的内部包含另一个事物,那么这就是一个类内部包含另一个类。

分类：

1. 成员内部类
2. 局部内部类(包含匿名内部类)

### 成员内部类

成员内部类的定义

格式:

```java
修饰符 class 外部类名称(){
    修饰符class内部类名称(){
       //方法体 
    }
    //方法体
}
```

注意:内用外,随意访问:外用内,需要内部类对象。

编译后的文件夹有`内部类名$外部类名.class`、`内部类名.class`两个文件

**使用：**如何使用成员内部类?有两种方式:

**间接方式:**在外部类的方法当中,使用内部类:然后main只是调用外部类的方法。

**直接方式：**

格式：

`外部类名称.内部类名称 对象名 = new外部类名称().new内部类名称();`

内部类同名变量访问：如果出现了重名现象,那么格式是:`外部类名称.this.外部类成员变量名`

```java
package neibulei;

public class Nei {

    int num=10;

    public class ZiNei{

        int num = 20;

        public void show(){
            int num = 30;
            System.out.println(num);//就近原则访问
            System.out.println(this.num);//访问本类成员变量
            System.out.println(Nei.this.num);//访问外部类成员变量
        }
    }

    public void show(){
        System.out.println("外部类方法");
    }
}
```

```java
package neibulei;

public class Implementation {
    public static void main(String[] args) {
        Nei.ZiNei obj = new Nei().new ZiNei();
        obj.show();
    }
}
```

### 局部类：

如果一个类是定义在一个方法内部的,那么这就是一个局部内部类。

“局部”,只有当前所属的方法才能使用它,出了这个方法外面就不能用了。

**定义格式:**

```java
修饰符 class 外部类名称{
    修饰符 返回值类型 外部类方法名称(参数列表) {
        //方法体
        class 局部内部类名称{
            //类中的各种
        }
    }
}
```

**使用方法：**

```java
修饰符 class 外部类名称{
    修饰符 返回值类型 外部类方法名称(参数列表) {
        //方法体
        class 局部内部类名称{
            //类中的各种
        }
        局部内部类名称 对象名 = new 局部内部类名称();
        对象名.局部内部类中方法；
    }
}
```

定义一个类的时候,权限修饰符规则:

1. 外部类: public / (default)
2. 成员内部类: public / protected / (default) / private
3. 局部内部类:什么都不能写

### 局部内部类

局部内部类,如果希望访问所在方法的局部变量,那么这个局部变量必须是【有效final的】。访问所在方法的局部变量

备注:从Java 8+开始,只要局部变量事实不变,那么final关键字可以省略。

原因；

1. new出来的对象在堆内存当中。
2. 局部变量是跟着方法走的,在栈内存当中。
3. 方法运行结束之后,立刻出栈,局部变量就会立刻消失。
4. 但是new出来的对象会在堆当中持续存在,直到垃圾回收消失。

### 匿名内部类

如果接口的实现类(或者是父类的子类)只需要使用唯一的一次,

那么这种情况下就可以省略掉该类的定义,而改为使用【匿名内部类】

匿名内部类的定义格式

```java
接口名称 对象名 = new 接口名称(){
    //覆盖重写所有抽象方法
};
```

```java
public interface NiMing {
    public abstract void show();
}
```

```java
public class NiMingLei {
    public static void main(String[] args) {
        NiMing obj = new NiMing() {
            @Override
            public void show() {
                System.out.println("匿名内部类");
            }
        };
        obj.show();
    }
}
```

==匿名对象直接在后面点方法名`new 类名（）.方法名`匿名对象调用方法只能调用一次==

对格式“new接口名称() (..)"进行解析

1. new代表创建对象的动作
2. 接口名称就是匿名内部类需要实现哪个接口
3. (..)这才是匿名内部类的内容

另外还要注意几点问题;

1. 匿名内部类,在【创建对象】的时候,只能使用唯一一次。如果希望多次创建对象,而且类的内容一样的话,那么就必须使用单独定义的实现类了。
2. 匿名对象,在【调用方法】的时候,只能调用唯一—次。如果希望同一个对象,调用多次方法,那么必须给对象起个名字。
3. 匿名内部类是省略了【实现类/子类名称】,但是匿名对象是省略了【对象名称】

**强调：**,匿名内部类和匿名对象

## Object类

### toString方法

打印地址值

使用需要重写toString方法，要看是否重写了toString方法就new该对象，然后输出。

1. toString方法会返回一个“以文本方式表示”此对象的字符串。结果是一个简明但易于读懂的信息表达式。建议所有子类都重写此方法。

Object类是toString方法返回一个字符串，该字符串由类名（对象是该类的一个实例）、at标记符“@”和此对象哈希码的无符号十六进制表示组成。换句话说，该方法返回一个字符串，它的值等于：

```
getClass().getName()+``'@'``+Integer.toHexString(hashCode())；
```

返回：该对象的字符串表示形式

2. 因为它是Object里面已经有了的方法，而所有类都是继承Object，所以“所有对象都有这个方法”；

它通常只是为了方便输出，比如`System.out.println(xx)`，括号里面的“xx”如果不是String类型的话，就自动调用xx的`toString()`方法；

总而言之，它只是sun公司开发java的时候为了方便所有类的字符串操作而特意加入的一个方法。



### equals方法

所有类默认继承了object类,所以可以使用Object类的equals方法

boolean equals(Object obj)指示其他某个对象是否与此对象"相等”。

Object类equals方法的源码:

```java
public boolean equals(Object obj){ 
    return (this == obj)
};
```

**参数:**object obj:可以传递任意的对象

**方法体:**

`==`比较运算符,返回的就是一个布尔值 true, false

基本数据类型:比较的是值

引用数据类型:比较的是两个对象的地址值

this是谁?那个对象调用的方法,方法中的this就是那个对象;p1调用的equals方法,所以this就是P1

obj是谁?传逐过来的参数p2

this == obj  --->  pl==p2

**重写equals方法：**

```java
//比较两个对象的属性
@Override
public boolean equals(Object obj){
    //向下转型
    //本类 对象名 = (本类名)obj
    Person p = (Person)obj;
    boolean b = this.name.equals(p.name) && this.age.equals(p.age);
    return b;
}
```

**重点：**空null不能调用方法

1. Object类介绍Object类是所有类的父类。一个类都会直接或者间接的继承自该类该类中提供了一些非常常用的方法!

2. toString()方法

   A:作用:打印对象的信息

   B:重写前:打印的是包名类名@地址值

   C:重写后:打印的是对象中的属性值

3. equals()方法

   A:作用:比较两个对象的

   B:重写前:比较的是对象的地址值

   C:重写后:比较的是对象中的属性值

4. Objects类

   1. equals()方法比较两个对象是否相同,但是加了一些健壮性的判断!

### Date类

**空参数构造方法**：

Date()获取的就是当前系统的日期和时间

```java
package Date;

import java.util.Date;

public class Mode01 {
    public static void main(String[] args) {
        mode01();
        mode02();
        mode03();
    }
    //Date类的成员方法Long getTime()
    // 把日期转换为秒(相当于System.currentTimeMillis())
    // 返回自1970年1月1日00:00:00 GMT以来此Date对象表示的毫秒数。
    private static void mode03() {
        Date date = new Date();
        long time = date.getTime();
        System.out.println(time);
    }

    //Date类的带参数构造方法:Date(Long date)
    // 传递毫秒值,把毫秒转换为Date日期
    private static void mode02() {
        Date date = new Date(0l);
        System.out.println(date);
        Date date1 = new Date(125715141317l);
        System.out.println(date1);
    }
    //Date类的空数构造方法:Date()获取的就是当前系统的日期和时间
    public static void mode01() {
        Date date = new Date();
        System.out.println(date);
    }
}
```

### DateFormat类

`java.text.DateFormat`是日期/时间格式化子类的抽象类,我们通过这个类可以帮我们完成日期和文本之间的转换,也就是可以在Date对象与String对象之间进行来回转换。

* 格式化:按照指定的格式,从Date对象转换为String对象。
* 解析:按照指定的格式,从String对象转换为Date对象。

DateFormat是日期/时间格式化子类的抽象类,它以与语言无关的方式格式化并解析日期或时间。格式化子类（如SimpleDateFormat)允许进行格式化(也就是日期->文本)、解析(文本->日期)和标准化。将日期表示为Date对象,或者表示为从GMT (格林尼治标准时间) 1970年1月1日00:00:00这一刻开始的毫秒数。

作用:格式化(也就是日期->文本)、解析(文本->日期)

成员方法:

* String format(Date date) 按照指定的模式,把0ate日期,格式化为符合模式的字符串
* Date parse(String source)把符合模式的字符串,解析为Date日期

DateFormat类是一个抽象类,无法直接创建对象使用,可以使用DateFormat的子类java.text.SimpleDateFormat

| 标识字母（区分大小写） | 含义 |
| ---------------------- | ---- |
| y                      | 年   |
| M                      | 月   |
| d                      | 日   |
| H                      | 时   |
| m                      | 分   |
| s                      | 秒   |

写对应的模式,会把模式替换为对应的日期和时间

"Уyyy-MM-dd HH:mm:SS""yyyy年MM月da日 HH时mm分ss秒"

注意:模式中的字母不能更改,连接模式的符号可以改变

```java
package Date;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Scanner;

public class Mode03 {
    public static void main(String[] args) throws ParseException {
        //1.使用Scanner类中的方法next,获取出生日期
        Scanner scanner = new Scanner(System.in);
        System.out.println("请输入你的年龄：格式：yyyy--MM--dd");
        String str = scanner.next();
        //2,使用DateFormat类中的arse,把字符串的出生日期解析为Date格式
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy--MM--dd");
        //3.把String类型转换为Date格式
        Date date = simpleDateFormat.parse(str);
        //3.把Date格式的出生日期转换为毫秒值
        long date1 = date.getTime();
        //获取当前时间并转换为毫秒值
        long date2 = new Date().getTime();
        //用当前时间减去输入的时间
        long test = date2 - date1;
        //test/1000/60/60/24/365将毫秒值转换为年
        System.out.println("你现在已经"+test/1000/60/60/24/365+"岁");
    }
}
```

### Calendar类

日历类

Calendar类是一个抽象类,它为特定瞬间与一组诸如YEAR、MONTH、DAY_OF_MONTH、 HOUR等日历字段之间的转换提供了一些方法,并为操作日历字段(例如获得下星期的日期)提供了一些方法。瞬间可用毫秒值来表示,它是距历元(即格林威治标准时间1970年1月1日的00:00:00.000,格里高利历)的偏移量。

与其他语言环境敏感类一样,Calendar提供了一个类方法getInstance,以获得此类型的一个通用的对象。Calendar的getInstance方法返回一个Calendar对象,其日历字段已由当前日期和时间初始化:

`Calendar rightNow = Calendar.getInstance ():`

根据Calenda类的API文档,常用方法有:

* `public int get(int field)` :返回给定日历字段的值。

* `public void set(int field, int value) `:将给定的日历字段设置为给定值。

* `public abstract void add(int field, int amount)` :根据日历的规则,为给定的日历字段添加或减去指定的时间量。

* `public Date getTime() :`返回一个表示此Calendar时间值(从历元到现在的毫秒偏移量)的Date对象。

Calendar类中提供很多成员常量,代表给定的日历字段:

| 字段值       | 含义                      |
| ------------ | ------------------------- |
| YEAR         | 年                        |
| MONTH        | 月（从0开始，可以+1使用） |
| DAY_OF_MONTH | 月中的几天（几号）        |
| HOUR         | 时（12小时制）            |
| HOUR_OF_DAY  | 时（24小时制）            |
| MINUTE       | 分                        |

```JAVA
java.util.GregorianCalendar[time=1655449507745,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2022,MONTH=5,WEEK_OF_YEAR=25,WEEK_OF_MONTH=3,DAY_OF_MONTH=17,DAY_OF_YEAR=168,DAY_OF_WEEK=6,DAY_OF_WEEK_IN_MONTH=3,AM_PM=1,HOUR=3,HOUR_OF_DAY=15,MINUTE=5,SECOND=7,MILLISECOND=745,ZONE_OFFSET=28800000,DST_OFFSET=0]
```

int field:日历类的字段,可以使用calendar类的静态成员变量获取

```JAVA
public static final int YEAR = 1; 年 
public static final int MoNTH = 2; 月
public static final int DATE = 5; 月中的某一天
public static final int DAY_OF_MONTH = 5;月中的某一天
public static final int HoUR = 10;
public static final int MINUTE = 12;
public static final int SECOND = 13;时分秒
```

```java
package Calendar;

import java.util.Calendar;
import java.util.Date;

public class Calendarc {

    public static void main(String[] args) {
        Calendar right = Calendar.getInstance();//返回子类对象
        /*
        public int get(int field)方法
        Calendar.YEAR获取静态属性
        public int get(int field):返回给定日历字段的值。
        参数:传递指定的日历字段(YEAR, MONTH...)
        返回值:日历字段代表具体的值
        */
        int a = right.get(Calendar.YEAR);
        System.out.println(a);
        int b = right.get(Calendar.MARCH);
        System.out.println(b+1);
        int c = right.get(Calendar.DAY_OF_MONTH);
        System.out.println(c);
        int d = right.get(Calendar.HOUR);
        System.out.println(d);
        int e = right.get(Calendar.MINUTE);
        System.out.println(e);
        int f = right.get(Calendar.SATURDAY);
        System.out.println(f);
        /*
        public void set(int field, int value):将给定的日历字段设置为给定值。
        参数:
        int field:传递指定的日历字段(YEAR, MONTH...)
        int value:传递的字段设置的具体的值
        * */
        right.set(Calendar.YEAR,1997);
        int aa = right.get(Calendar.YEAR);
        System.out.println(aa);
        right.set(Calendar.MARCH,5);
        right.set(Calendar.HOUR,11);
        int bb = right.get(Calendar.MARCH);
        System.out.println(bb+1);
        int dd = right.get(Calendar.HOUR);
        System.out.println(dd);
        //同时设置年月日,可以使用set的重载方法

        right.set(1997,11,12);
        int cc = right.get(Calendar.YEAR);
        System.out.println(cc);
        int zz = right.get(Calendar.MARCH);
        int xx = right.get(Calendar.HOUR);
        xx=xx+1;
        System.out.println(cc+","+zz+","+xx);
        /*
        public abstract void add(int field, int amount):根据日历的规则,为给定的日历字段添加或减去指定的时间量。
        把指定的字段增加/减少指定的值参数:
        int field:传递指定的日历字段(YEAR, MONTH...)
        int amount :增加/减少的值正数:增加负数:减少
        * */
        right.add(Calendar.YEAR,2);
        int ccc = right.get(Calendar.YEAR);
        System.out.println(ccc);
        /*
        public Date getTime():返回一个表示此calendar时间值(从历元到现在的毫秒偏移量)的Date对象。
        把日历对象,转换为日期对象
        * */
        Date date = right.getTime();
        System.out.println(date);
    }
}
```

### System类

java.lang.System类中提供了大量的静态方法,可以获取与系统相关的信息或系统级操作,在System类的API文档中,常用的方法有:

* public static long currentTimeMillis() :返回以毫秒为单位的当前时间。
* public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)将数组中指定的数据拷贝到另一个数组中

```java
package Calendar.System;

public class Test01 {
    public static void main(String[] args) {
        //程序执行一次耗费多少毫秒
        long s =System.currentTimeMillis();
        for (int i =0 ; i <= 9999; i++){
            System.out.println(i);
        }
        long x =System.currentTimeMillis();
        System.out.println(x-s);
        /*
        public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length):
        参数:
        将数组中指定的数据拷贝到另一个数组中。
        src-源数组。
        srcPos -源数组中的起始位置。
        dest -目标数组。
        destPos -目标数据中的起始位置。
        Length-要复制的数组元素的数量。
        * */
        int[] a = new int[]{1,2,3,4};
        int[] c = new int[5];
        System.arraycopy(a,0,c,1,4);
        for (int i = 0; i < c.length; i++) {
            System.out.print(c[i]);
        }
    }
}
```

### StringBuilder原理

String类代表字符串。Java程序中的所有字符串字面值(如"abe" )都作为此类的实例实现。

字符串是常量;它们的值在创建之后不能更改。字符串缓冲区支持可变的字符串。因为String对象是不可变的,所以可以共享。例如:

`String str = "abc";`等效于:`char data[] = ['a', 'b', 'c'];String str = new String (data);`

宇符串是常量;它们的值在创建之后不能更改。字符串的底层是一个被final修饰的数组,不能改变,是一个常量private final byte[] value;



StringBuilder类字符串缓冲区,可以提高字符串的操作效率(看成一个长度可以变化的字符串)底层也是一个数组,但是没有被final修饰,可以改变长度`byte[] value = new byte[16];`

StringBuilder在内存中始终是一个数组,占用空间少,效率高如果超出了StringBuilder的容量,会自动的扩容

根据StringBuilder的API文档,常用构造方法有2个:

* public StringBuilder() :构造-空的StringBuilder容器。
* public StringBuilder(String str) :构造一个StringBuilder容器,并将字符串添加进去。

```java
package Calendar.System;

public class test02 {
    public static void main(String[] args) {
        StringBuilder builder = new StringBuilder();
        System.out.println(builder);
        StringBuilder builder1 = new StringBuilder("fhgfh");
        System.out.println(builder1);
    }
}
```

StringBuilder常用的方法有2个:

* `public StringBuilder append(...)` :添加任意类型数据的字符串形式,并返回当前对象自身。

* `public String toString() :`当前StringBuilder对象转换为String对象。

append方法

append方法具有多种重载形式,可以接收任意类型的参数。任何数据作为参数都会将对应的字符串内容添加到StringBuilder中。例如:

```java
public class Test03 {
    public static void main(String[] args) {
        StringBuilder but1 = new StringBuilder();
        but1.append("abs");
        System.out.println(but1);
        //链式编程:方法的返回值是一个对象,可以根据对象继续调用方法
        System.out.println("abc".toUpperCase().toLowerCase().toUpperCase(). toLowerCase(). toUpperCase());
        but1.append ("abc") . append (1) . append (true) . append (8.8) . append (12);
        System.out.println(but1);
    }
}

```

reverse()

```java
but1.reverse();//反转字符串
System.out.println(but1);
```

tostring()

StringBuilder和String可以相互转换:

String->StringBuilder:可以使用StringBuilder的构造方法StringBuilder(String str)构造一个字符串生成器,并初始化为指定的字符串内容。StringBuilder->String:可以使用StringBuilder中的tostring方法public String tostring():当前StringBuilder对象转换为String对象。

```java
package Calendar.System;

import java.util.Arrays;

public class Test05 {
    public static void main(String[] args) {
        String str = "hello";
        //将String转换为StringBuilder
        StringBuilder sb = new StringBuilder(str);
        System.out.println(sb);
        //向对象中添加数据
        sb.append("word");
        //将StringBuilder转换为String
        String b = sb.toString();
        System.out.println(b);
    }
}
```

## 包装类

Java提供了两个类型系统,基本类型与引用类型,使用基本类型在于效率,然而很多情况,会创建对象使用,因为对象可以做更多的功能,如果想要我们的基本类型像对象一样操作,就可以使用基本类型对应的包装类,如下:

| 基本类型 | 对应的包装类(位于java.lang包中) |
| -------- | ------------------------------- |
| byte     | Byte                            |
| short    | Short                           |
| int      | Integer                         |
| long     | Long                            |
| floa     | Float                           |
| double   | Double                          |
| char     | Character                       |
| boolean  | Boolean                         |

装箱:把基本类型的数据,包装到包装类中(基本类型的数据->包装类)

构造方法:

* Integer(int value)构造一个新分配的Integer 对象,它表示指定的int值。
* Integer(String s)构造一个新分配的Integer对象,它表示String参数所指示的int值。

传递的字符串,必须是基本类型的字符串,否则会抛出异常“100"正确 "a"抛异常

静态方法:

* static Integer valueOf(int i)返回一个表示指定的int 值的Integer 实例。
* static Integer valueOf(String s)返回保存指定的String 的值的Integer对象。

拆箱:在包装类中取出基本类型的数据(包装类->基本类型的数据)

成员方法:

* int intValue()以int型返回 Integer的值。

```java
package baozhuanglei;

public class Test01 {
    public static void main(String[] args) {
        //装箱
        Integer str =  new Integer(1);
        System.out.println(str);
        Integer str1 =  new Integer("1");
        System.out.println(str1);
        Integer str2 = Integer.valueOf(1);
        System.out.println(str2);
        Integer str3 =Integer.valueOf("1");
        System.out.println(str3);
        //拆箱
        int str4 = str3.intValue();
        System.out.println(str4);
    }
}
```

### 自动装箱与自动拆箱

由于我们经常要做基本类型与包装类之间的转换,从Java 5 (JDK 1.5)开始,基本类型与包装类的装箱、拆箱动作可以自动完成。例如:

```java
Integer i = 4;//自动装箱。当于Integer i = Integer.valueof (4);
i =i+ 5;//等号右边:将i对象转成基本数值(自动拆箱) i.intValue() + 5;
//加法运算完成后,再次装箱,把基本数值转成对象。
```

## 集合

### Collection集合

集合:集合是java中提供的一种容器,可以用来存储多个数据。集合和数组既然都是容器,它们有啥区别呢?

* 数组的长度是固定的。==集合的长度是可变的。==
* 数组中存储的是同一类型的元素,可以存储基本数据类型值。==集合存储的都是对象==。而且对象的类型可以不一致。在开发中一般当对象多的时候,使用集合进行存储。

#### 集合框架

JAVASE提供了满足各种需求的API,在使用这些API前,先了解其继承与接口操作架构,才能了解何时采用哪个类,以及类之间如何彼此合作,从而达到灵活应用。

集合按照其存储结构可以分为两大类,分别是==单列集合==`java.util.Collection`和==双列集合==`java.util.Map`,今天我们主要学习Collection集合,在day04时讲解Map集合。

* Collection :单列集合类的根接口,用于存储一系列符合某种规则的元素,它有两个重要的子接口,分别是`java.util.List`和`java.util.Set` 。其中, `List`的特点是元素有序、元素可重复。`Set`的特点是元素无序,而且不可重复。`List`接口的主要实现类有`java.util.Arraylist` 和`java.util.LinkedList`,`Set`接口的主要实现类有`java.util.HashSet` 和`java.util.TreeSet`。从上面的描述可以看出JDK中提供了丰富的集合类库,为了便于初学者进行系统地学习,接下来通过一张图来描述整个集合类的继承体系。

```mermaid
 graph TB
        A[Collection]
        style A fill:orange
        B[List]
        style B fill:orange
        C[Set]
        style C fill:orange
        A---B
        A---C
        F[ArrayList]
        style F fill:#10c5f8
        G[LinkList]
        style G fill:#10c5f8
        H[Vector]
        style H fill:#10c5f8
        I[HashSet]
        style I fill:#10c5f8
        J[LinkedHashSet]
        style J fill:#10c5f8
        K[TreeSet]
        style K fill:#10c5f8
        B---F
        B---G
        B---H
        C---I
        I---J
        C---K
        subgraph Integer
        D[e]
        end
        style D fill:orange
        subgraph Class
        E[e]
        end
        style E fill:#10c5f8
```

#### 集合框架的学习方式:

1.学习顶层:学习顶层接口/抽象类中共性的方法所有的子类都可以使用

2.使用底层:底层不是接口就是抽象类,无法创建对象使用,需要使用底层的子类创建对象使用

**Collection接口**

* 定义的是所有单列集合中共性的方法
* 所有的单列集合都可以使用共性的方法
* 没有带索引的方法

**List接口**

1. 有序的集合(存储和取出元素顺序相同)
2. 允许存储重复的元素
3. 有索引,可以使用普通的for循环遍历

* ArrayList :底层是数组实现的,查询快、增删慢

* LinkedList:底层是链表实现的,查询慢、增删快

**Set接口**

1. 不允许存储重复元素
2. 没有索引(不能使用普通的for循环遍历)
3. 无序的集合(存健和取出元素的顺序有可能不一致)

* HashSet:底层是哈希表+(红黑树)实现的,无索引、不可以存储重复元素、存取无序

* LinkedHashSet :底层是哈希表+链表实现的,无索引、不可以存储重复元素、可以保证存取顺序

* TreeSet:底层是二叉树实现。一般用于排序

**Collection集合常用方法**

1. boolean add(E e);                       向集合中添加元素
2. boolean remove(E e);                 删除集合中的某个元素
3. void clear()；                                清空集合所有的元素
4. boolean contains(E e);                判断集合中是否包含某个元素
5. boolean isEmpty0;                      判断集合是否为空
6. int size();                                       获取集合的长度
7. Object[] toArray();                       将集合转成一个数组

```java
package Calendar.jihe;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collection;

public class Test01 {
    public static void main(String[] args) {
        Collection<String> collection = new ArrayList<>();
        //添加
        collection.add("a");
        collection.add("b");
        collection.add("c");
        collection.add("d");
        collection.add("e");
        System.out.println(collection);
        //删除
        collection.remove("a");
        System.out.println(collection);
        //清空
        collection.clear();
        System.out.println(collection);
        //添加
        collection.add("a");
        collection.add("b");
        collection.add("c");
        collection.add("d");
        collection.add("e");
        System.out.println(collection);
        //断集合中是否包含某个元素
        System.out.println(collection.contains("c"));
        //判断集合是否为空
        boolean s = collection.isEmpty();
        System.out.println(s);
        //获取集合的长度
        int a = collection.size();
        System.out.println(a);
        //将集合转成一个数组
        /*
        Object[] arr = collection.toArray();
        */
        System.out.println(Arrays.toString(collection.toArray()));
    }
}
```

#### Iterator接口

在程序开发中,经常需要遍历集合中的所有元素。针对这种需求,JDK专门提供了一个接口java.util.Iterator。Iterator接口也是Java集合中的一员,但它与Collection、Map接口有所不同,Collection接口与Map接口主要用于存储元素,而Iterator主要用于选代访问(即遍历) Collection中的元素,因此Iterator对象也被称为选代器。

想要遍历Collection集合,那么就要获取该集合迭代器完成选代操作,下面介绍一下获取迭代器的方法:

* `public Iterator iterator()` :获取集合对应的迭代器,用来遍历集合中的元素的。

### List集合

`java.util.List`接口继承自`Collection`接口,是单列集合的一个重要分支,习惯性地会将实现了`List`接口的对象称为List集合。在List集合中允许出现重复的元素,所有的元素是以一种线性方式进行存储的,在程序中可以通过索引来访问集合中的指定元素。另外, List集合还有一个特点就是元素有序,即元素的存入顺序和取出顺序一致。

* List接口特点：

  1. 它是一个元素存取有序的集合。例如,存元素的顺序是11、22、33,那么集合中,元素的存储就是按照11、22、33的顺序完成的。
  2. 它是一个带有索引的集合,通过索引就可以精确的操作集合中的元素(与数组的索引是一个道理)。
  3. 集合中可以有重复的元素,通过元素的equals方法,来比较是否为重复的元素。

  #### List接口中常用方法

  List作为Collection集合的子接口,不但继承了Collection接口中的全部方法,而且还增加了一些根据元素索引来操作集合的特有方法，如下：

  1. `public void add(int index, E element)`:将指定的元素，添加到该集合中的指定位置上。

  2. `public E get(int index)` :返回集合中指定位置的元素。

  3. `public E remove(int index)` :移除列表中指定位置的元素,返回的是被移除的元素。

  4. `public E set(int index, E element)` :用指定元素替换集合中指定位置的元素,返回值的更新前的元素。

     注意：操作索引防止越界异常

     ```java
     public class ListDemo{
         public static void main(String[] args){
             //创建List集合对象
             List<String> list = new ArrayList<String>();
             //往尾部添加指定元素
             list.add("");
             //往指定位置添加指定元素
             list.add(1,"");
             //移除列表中指定位置的元素
             list.remove();
             //用指定元素替换集合中指定位置的元素
             list.set(1,""); 
         }
     }
     ```

  #### List遍历

  `public E get(int index)` :返回集合中指定位置的元素。

  1. 普通for循环

     ````java
     for(int i=0;i<list.size();i++){
         String s = list.gir(i);
         System.out.println(s);
     }
     ````

  2. 迭代器

     ```java
     Iterator<String> it = list.iterator();
     while(it.hasNext()){
         String s = list.gir(i);
         System.out.println(s);
     }
     ```

  3. 增强for循环

     ```java
     for(String s : list){
         System.out.println(s);
     }
     ```

### Arraylist集合

`java.util.ArrayList` 集合数据存储的结构是数组结构。元素增删慢，查找快，由于日常开发中使用最多的功能为查询数据、遍历数据,所以ArrayLilst是最常用的集合。许多程序员开发时非常随意地使用ArrayList完成任何需求,并不严谨,这种用法是不提倡的。

### LinkedList集合

`java.util.LinkedList` 集合数据存储的结构是链表结构。方便元素添加、删除的集合。

1. 常用方法
   * `public void addFirst(E e)`：将指定元素插入此列表的开头。
   * `public void addLast(E e)`：将指定元素添加到此列表的结尾。
   * `public E getFirst()`：返回此列表的第一个元素。
   * `public E getLast()`：返回此列表的最后一个元素。
   * `public E removefirst()`：移除并返回此列表的第一个元素。
   * `public E removeLast()`:移除并返回此列表的最后一个元素。
   * `public E pop()`：从此列表所表示的堆栈处弹出一个元素。
   * `public void push(E e)`：将元素推入此列表所表示的堆栈。
   * `Ipublic boolean isEmpty()`：如果列表不包含元素，则返回true。

### 哈希值

* 哈希表是由数组+链表+红黑树实现的。
  1. 哈希值:是一个十进制的整数,由系统随机给出(就是对象的地址值,是一个逻辑地址,是模拟出来得到地址,不是数据实际存储的物理地址)在object类有一个方法,可以获取对象的哈希值
     * int hashCode()返回该对象的哈希码值。
     * hashCode方法的源码：public native int hashCode();
     * native：代表该方法调用的是本地操作系统的方法
  2. toString方法的源码
     * return getClass().getName()+“@”+Integer.toHexString(hashCode());
  3. String类的哈希值
     * String类重写Object类的hashCode方法

#### HashSet集合

1. 介绍

   1. Set接口的特点：

      1. 不允许存储重复元素
      2. 没有索引，没有带索引的方法，也不能使用普通for循环遍历

   2. java.util.HashSet集合 implements Set接口

      * HashSet特点：

      1. 不允许存储重复元素

      2. 没有索引，没有带索引的方法，也不能使用普通for循环遍历

      3. 是一个无序集合，存储元素和取出元素的顺序有可能不一致

      4. 底层是一个哈希结构表（查询速度非常快）

         ```java
         Set<Integer> set = new HashSet<>();
         //使用add方法往集合中添加元素
         set.add(1);
         set.add(3);
         set.add(2);
         set.add(1);
         //使用迭代器变量set集合
         Iterator<Integer> it = set.iterator();
         where(it.hasNext()){
             Interator n = it.next();
             System.out.println(n);//123
         }
         //使用增强for循环遍历set集合
         for (Integer i : set){
             System.out.println(i);
         }
         ```

2. HashSet存储数据结构

   1. 哈希表
      * 哈希表初始容量为16
      * 数组结构：把元素进行了分组，（想同哈希值的元素是一组）；链表/红黑树：把相同哈希值的元素连接到一起
      * 如果链表的长度超过了8位，那么会把链表转换为红黑树（提高查询速度）

3. Set集合不重复原理

   1. Set集合在调用add方法时，add方法会调用元素的hashCode方法和equals方法，判断元素是否重复
      * 先判断哈希值是否相同，哈希值不同存入集合
      * 哈希值相同在判断元素是否相同，元素相同不存入集合，不同存入集合

4. HashSet存储自定义类型元素

   1. 给HashSet中存放自定义类型元素时,需要重写对象中的hashCode和equals方法,建立自己的比较方式,才能保证HashSet集合中的对象唯一

5. LinkedHashSet集合

   1. java.util.LinkedHashSet集合 extends HashSet集合
   2. LinkedHashSet集合特点：
      * 底层是一个哈希表（数组+链表/红黑树）+链表：多了一条链表（记录元素的存储顺序），保证元素有序

6. 可变参数

   1. 使用前提：

      * 当方法的参数列表数据类型已经确定,但是参数的个数不确定,就可以使用可变参数。

   2. 使用格式:定义方法时使用

      * `修饰符 返回值类型 方法名（数据类型...变量名）{}`

   3. 可变參数的原理：

      * 可变参数底层就是一个数组,根据传递参数个数不同,会创建不同长度的数组,来存储这些参数传递的参数个数，可以是一个（不传递），1,2...多个

      ```java
      public class Demo{
          public static void main(String[] args){
              int i = ace(10,20);
              System.out.pringln(i);
          }
          
          publi static int ace(int...arr){
              int sum = 0;
              for (int i : arr){
                  sum += i;
              }
              return sum;
          }
      }
      ```

   4. 可变參数的注意事项

      1. 一个方法的参数列表，只能有一个可变参数

      2. 如果方法的参数有多个，那么可变参数必须写在参数列表的末尾

         ```java
         publi static int ace(String b,int...arr){}
         publi static int ace(Object...obj){}
         ```

### Collections集合

1. 工具类的方法
   * addAll
   * shuffle

### Map集合



## 迭代

迭代:==即Collection集合元素的通用获取方式。在取元素之前先要判断集合中有没有元素,如果有,就把这个元素取出来,继续在判断,如果还有就再取出出来。一直把集合中的所有元素全部取出。这种取出方式专业术语称为迭代。==

Iterator接口的常用方法如下:

* `public E next();`返回选代的下一个元素。

* `public boolean hasNext();`如果仍有元素可以选代,则返回 true。

Iterator迭代器,是一个接口,我们无法直接使用,需要使用Iterator接口的实现类对象,获取实现类的方式比较特殊

collection接口中有一个方法,叫iterator(),这个方法返回的就是选代器的实现类对象

`Iterator<E> iterator()`返回在此collection 的元素上进行选代的选代器。

迭代器的使用步骤(重点):

1. 使用集合中的方法iterator()获取选代器的实现类对象,使用Iterator接口接收(多态)
2. 使用Iterator接口中的方法hasNext判断还有没有下一个元素
3. 使用Iterator接口中的方法next取出集合中的下一个元素

```java
package Calendar.jihe.diedia;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;

public class Testo1 {
    public static void main(String[] args) {
        Collection<String> collection = new ArrayList<>();
        collection.add("a");
        collection.add("b");
        collection.add("c");
        collection.add("d");
        collection.add("e");
        /*
        Iterator<E>接口也是有泛型的,选代器的泛型跟着集合走,集合是什么泛型,选代器就是什么泛型
        多态 接口 实现类
        * */
        Iterator<String> arr = collection.iterator();
        for (int i = 0; i < collection.size(); i++) {
            if (arr.hasNext()){
                System.out.println(arr.next());
            }
        }
        while (arr.hasNext()){
            System.out.println(arr.next());
        }
    }
}
```

### 增强for循环

增强for循环(也称for each循环)是 JDK1.5 以后出来的一个高级for循环,专门用来遍历数组和集合的。它的内部原理其实是个Iterator选代器,所以在遍历的过程中,不能对集合中的元素进行增删操作。

`collection<E>extends Iterable<E>` :所有的单列集合都可以使用增强for
`public interface Iterable<T>`实现这个接口允许对象成为"foreach"语句的目标。

```java
for(元素数据类型 变量：Collection集合 or 数组){
    //代码块
}
```

```java
//使用增强for循环遍历集合
    public static void demo01() {
        ArrayList<String> lits = new ArrayList();
        lits.add("a");
        lits.add("b");
        lits.add("c");
        lits.add("d");
        for (String s : lits) {
            System.out.println(s);
        }
    }

    //使用增强for循环遍历数组
    public static void demo02() {
        int[] arr = {1, 2, 3, 4, 5, 6};
        for (int s : arr) {
            System.out.println(s);
        }
    }
```

## 泛型

泛型:是一种未知的数据类型,当我们不知道使用什么数据类型的时候,可以使用泛型泛型也可以看出是一个变量,用来接收数据类型

* E e: Element元素
* T t: Type类型

ArrayList集合在定义的时候,不知道集合中都会存储什么类型的数据,所以类型使用泛型

E:未知的数据类型

```java
public class ArrayList<E>{
    public boolean add(E e) {}
    public E get(int index){}
}
```

创建集合对象的时候,就会确定泛型的数据类型`ArrayList<String> list = new ArrayList<String>();`

会把数据类型作为参数传递,把String赋值给泛型E

```java
public class ArrayList<String>{
    public boolean add(String e) {}
    public String get(int index){}
}
```

`ArrayList<Student> list= new ArrayList<Student>;`

会把数据类型作为参数传递,把Student赋值给泛型E

```java
public class ArrayList<Stusent>{
    public boolean add(Stusent e) {}
    public Stusent get(int index){}
}
```

### 创建集合对象,使用泛型

好处:

1. 避免了类型转换的麻烦,存储的是什么类型,取出的就是什么类型
2. 把运行期异常(代码运行之后会抛出的异常),提升到了编译期(写代码的时候会报错)

弊端:

泛型是什么类型,只能存储什么类型的数据

```java
package enhanceFor.Generic;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;
public class TheGeneric {
    public static void main(String[] args) {
        //使用泛型
        show01();
        //不使用泛型
        //show02();
    }
    //使用泛型
    private static void show01() {
        ArrayList<String> list = new ArrayList();
        list.add("abc");
        //list.add(1);Yadd(java.Lang.String)in Arraylist cannot be applied to (int)
    }
    //不使用
    private static void show02() {
        ArrayList list = new ArrayList();
        list.add("abc");
        list.add(1);
        //使用送代器遍历List集合
        // 获取选代器
        Iterator arr = list.iterator();
        while (arr.hasNext()){
            //取出元素也是Object类型
            Object obj = arr.next();
            System.out.println(obj);
            //想要使用String类特有的方法,Length获取字符串的长度;不能使用 多态 Object obj = "abc";
            // 需要向下转型
            String s = (String)obj;
            System.out.println(s.length());
        }
    }
}
```

### 定义和使用含有泛型的类

定义格式:

```java
修饰符 class 类名<代表泛型的变量>{}
```

定义一个含有泛型的类,模拟ArrayList集合泛型是一个未知的数据类型,当我们不确定什么什么数据类型的时候,可以使用泛型泛型可以接收任意的数据类型,可以使用Integer,String, Student...创建对象的时候确定泛型的数据类型

```java
package enhanceFor.Generic;

public class GenericClass<E> {
    private E name;

    public E getName() {
        return name;
    }

    public void setName(E name) {
        this.name = name;
    }
}
```

```java
package enhanceFor.Generic;

public class GenericClassTest {
    public static void main(String[] args) {
        GenericClass gen = new GenericClass();
        gen.setName("afhgfjgfa");
        Object obj = gen.getName();
        System.out.println(obj);

        GenericClass<String> gen1 = new GenericClass();
        gen.setName("afhgfjgfa");
        Object obj1 = gen.getName();
        System.out.println(obj);

        GenericClass<Integer> gen2 = new GenericClass();
        gen.setName("afhgfjgfa");
        Object obj2 = gen.getName();
        System.out.println(obj);
    }
}
```

### 含有泛型的方法

定义格式:

```java
修饰符 <代表泛型的变量> 返回值类型 方法名(参数){}
```

含有泛型的方法,在调用方法的时候确定泛型的数据类型传递什么类型的参数,泛型就是什么类型

```javascript
package enhanceFor.Generic;

public class GenericMethodTest {
    public static void main(String[] args) {
        GenericMethod arr = new GenericMethod();
        arr.show01("qwe");
        arr.show01(1);
        //静态方法,通过类名,方法名(参数)可以直接使用
        GenericMethod.show02("qwe");
        GenericMethod.show02(12);
    }
}
```

```java
package enhanceFor.Generic;

public class GenericMethod {
    //含有泛型的方法
    public <M> void show01 (M m){
        System.out.println(m);
    }
    //含有泛型的静态方法
    public static <E> void show02 (E e){
        System.out.println(e);
    }
}
```

含有泛型的接口,第一种使用方式:定义接口的实现类,实现接口,指定接口的泛型

```java
public interface Iterator<E> { 
    E next();
}
```

Scanner类实现了Iterator接口,并指定接口的泛型为String,所以重写的next方法泛型默认就是String

`public final class Scanner implements Iterator<String>{}`

### 泛型通配符

当使用泛型类或者接口时，传递的数据中，泛型类型不确定，可以通过通配符<?>表示。但是一旦使用泛型的通配符后,只能使用Object类中的共性方法,集合中元素自身方法无法使用。

#### 通配符基本

使用泛型的通配符：**不知道使用什么类型来接收的时候，此时可以使用？，？表示未知通配符。**此时只能接受数据，不能往该集合中存储数据。

泛型没有继承概念的

```java
public class Demoe5Generic {
    public static void main(String[] args){
        ArrayList<Integer> liste1 = new ArrayList<>();
        liste1.add(1);
        list01.add(2);
        ArrayList<String> list02 = new ArrayList<>();
        list02.add("a");
        list02.add("b");
        printArray(list01);
        printArray(list02);
    }
    /*
    定义一个方法，能遍历所有类型的ArrayList集合这时候我们不知道ArrayList集合使用什么数据类型,可以泛型的通配符?来接收数据类型
    注意：泛型没有继承概念的
    */
    public static void printArray(ArrayList<?> list){
        //使用迭代器遍历集合1
        Iterator<?> it = list.iterator();
        while(it.hasNext()){
            //it.next()方法,取出的元素是Object,可以接收任意的数据类型
            Object o = it.next();
            System.out.println(o);
        }
}
```

#通配符高级使用----受限泛型

之前设置泛型的时候，实际上是可以任意设置的，只要是类就可以设置。但是在JAVA的泛型中可以指定一个泛型的==上限==和==下限==。

* 泛型的上限：
  * 格式: `类型名称<? extends 类 > 对象名称`
  * 意义：只能接收该类型及其子类
* 泛型的下限：
  * 格式：`类型名称<? super 类 > 对象名称`
  * 意义：只能接收该类型及其父类型

```java
public class Demoe6Generic {
    /*
    泛型的上限限定： ? extends E代表使用的泛型只能是E类型的子类/本身
    泛型的下限限定：? super E   代表使用的泛型只能是E类型的父类/本身
    */
    public static void main(String[] args){
        fCollection<Integer> list1 = new ArrayList<Integer>();
        Collection<String> list2 = new ArrayList<String>();
        Collection<Number> list3 = new ArrayList<Number>();
        Collection<Object> list4 = new ArrayList<object>();
        getELement1(list1);
        getElement1(list2);//报错
        getElement1(list3);
        getELement1(list4);//报错
        
        getElement2(list1);//报错
        getElement2(list2);//报错
        getElement2(list3);
        getElement2(list4);
        /*
        类与类之间的继承关系Integer extends Number extends Object String extends Object
        */
    }
    //泛型的上限:此时的泛型?,必须是Number类型或者Number类型的子类
    public static void getElement1(Collection<? extends Number> coll){}
    //泛型的下限:此时的泛型?,必须是Number类型或者Number类型的父类
    public static void getElement2(Collection<? super Number> coll){}
}
```

