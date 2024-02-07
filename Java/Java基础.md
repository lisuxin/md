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
