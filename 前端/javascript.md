[TOC]

# javascript

## 一、基础

代码书写位置

1. 行内式

   ```
   <body>
       <input type="button" value="点我" onclick="alert('行内式')">
   </body>
   ```

2. 内嵌式

   ```
   <head>
       <meta charset="UTF-8">
       <title>名字</title>
       <script>
           alert('内嵌式')
       </script>
   </head>
   ```

3. 外联式

   ```
   <head>
       <meta charset="UTF-8">
       <title>名字</title>
       <script src="test.js"></script>
   </head>
   ```

* JavaScript异步加载
  * async用于异步加载，即先下载文件，不阻塞其他代码执行`<script src="test.js" async></script>`
  * defer用于延后执行，即先下载文件，直到网页加载完成后再执行:`<script src="test.js" defer></script>`

1. 注释
   1. 单行注释`//`
   2. 多行注释`/*.......*/`
2. 输入输出
   1. 浏览器弹出警告框:`alert('msg')`
   2. 浏览器控制台输出信息:`console.log('msg')`  
   3. 浏览器弹出输入框，用户可以输入内容:`prompt('msg')`  

### 变量

var声明变量:变量初始化就是为变量赋一个值:在对变量进行命名时,需要遵循变量的命名规范,从而避免代码出错,以及提高代码的可读性,具体如下。

1. 变量命名规范
   * 由字母、数字、下划线和美元符号($)组成,如age、num。
   * 严格区分大小写,如app和App是两个变量。
   * 不能以数字开头,如18age是错误的变量名。
   * 不能是关键字、保留字,如var、for、while等是错误的变量名。
   * 要尽量做到“见其名知其意”,如age表示年龄, num表示数字。
   * 建议遵循驼峰命名法,首字母小写,后面的单词首字母大写,如myFirstNam e。 

###　数据类型

==JavaScript是一种弱类型语言，不用提前声明变量的数据类型。在程序运行过程中，变量的数据类型会被自动确定。==

==需要注意的是，代码中的值 true、false、undefined 和 null全部都要写成小写字母。==
$$
数据类型 \begin{cases} 基本数据类型 \begin{cases} \mathbf{Boolean(布尔型)} &\\ \mathbf{String(字符串类型)} &\\ \mathbf{Number(数字型)} &\\ \mathbf{Null(空)} & \\ \mathbf{Undefined(未定义型)} &\end{cases} & \\ 复杂数据类型\mathbf{Object(对象)} & \end{cases}
$$
1. 数字型（Number），包含整型值和浮点型值 :
   * JavaScript中的数字型可以用来保存整数或浮点数（小数）
     * `var num1 = 21; // 整型值`
     * `var num2 = 0.21; // 浮点型值`
   * 数字型的最大值和最小值可以用如下代码来获取。
     * `console.log(Number.MAX_VALUE);` // 输出结果：1.7976931348623157e+308
     * `console.log(Number.MIN_VALUE);` // 输出结果：5e-324
   * 数字型有3个特殊值，分别是Infinity（无穷大）、—Infinity（无穷小）、和NaN（Nota Number，非数值）若要判断一个变量是否为非数字的类型，可以用 isNaN()来进行判断，它会返回一个布尔值，返回 true表示非数字，返回 false表示是数字
2. 布尔型（Boolean），包含 true和 false两个布尔值 ：
   * `var bool1 = true;` // 表示真、1、成立
   * `var bool2 = false;` // 表示假、0、不成立
3. 字符串型（String），用单引号或双引号包裹 ：JavaScript中使用单引号或双引号:单双引号可以镶嵌
   * `var str1 = ''`; // 空字符串
   * `var str2 = 'abc';` // 单引号包裹的字符串 abc
   * `var str3 = "abc";` // 双引号包裹的字符串 abc
4. 未定义型（Undefined），只有一个值 undefined ：`var a; `// 声明变量 a，未赋值，此时 a就是 undefined；`var b = undefined;` // 变量 b的值为 undefined
5. 定型（Null），只有一个值 null：`var a = null;` // 变量 a的值为 null



#### 字符串转义符

| 转义符 | 解释说明                                               | 转义符 | 解释说明                                                 |
| :----: | ------------------------------------------------------ | :----: | -------------------------------------------------------- |
|  \\'   | 单引号                                                 |  \\"   | 双引号                                                   |
|   \n   | LF换行，n表示new line                                  |   \v   | 跳格（Tab,水平）                                         |
|   \t   | Tab符号                                                |   \r   | CR换行                                                   |
|   \f   | 换页                                                   |  \\\   | 反斜杠（\）                                              |
|   \b   | 退格，b表示blank                                       |   \0   | Null字节                                                 |
|  \xhh  | 由2位十六进制数字hh表示ISO-8859-1字符。如“\x61”表示“a” | \uhhhh | 由4位十六进制数字hhhh表示Unicode字符。如“\u597d”表示“好” |

1. 字符串长度：通过字符串的 length属性可以获取整个字符串的长度
   * `var str1 = 'I\'m a programmer';console.log(str1.length);` // 输出结果：16
   * `var str2 = ' 我是程序员';console.log(str2.length);` // 输出结果：5
2. 访问字符串中的字符:字符串可以使用“[index]”语法按照 index（索引）访问字符，index从 0 开始，一直到字符串的长度减 1，如果超过了 index最大值，会返回 undefined.
   * `var str = 'I\'m a programmer';`
   * console.log(str[0]); // 输出结果：I
   * console.log(str[1]); // 输出结果：'
   * console.log(str[15]); // 输出结果：r
   * console.log(str[16]); // 输出结果：undefined
3. 字符串拼接
   * 多个字符串之间可以使用“+”进行拼接，如果数据类型不同，拼接前会把其他类型转成字符串，再拼接成一个新的字符串。示例代码如下。
   * `console.log('a' + 'b');` // ab;`console.log('a' + 18);` // a18;`console.log('_' + true);` // _true;`console.log('12' + 14);` // 1214;`console.log(12 + 14);` // 两个数字相加，结果为 26（非字符串拼接）
   * 在实际开发中，经常会将字符串和变量进行拼接，这是因为使用变量可以很方便地修改里面的值。`var age = 18;``console.log(' 小明 ' + age + ' 岁');` // 小明 18岁
4. 数据类型检测:在开发中，当不确定一个变量或值是什么数据类型的时候，可以利用 typeof运算符进行数据类型检测。
   * `console.log(typeof 12);` // 输出结果：number

#### 数据类型转换

1. 转换为字符串型

   * 先准备一个变量：`var num = 3.14;`

   * 方式 1：利用"+"拼接字符串（最常用的一种方式）:`var str = num + '';`;`console.log(str, typeof str);` // 输出结果：3.14 string
   * 方式 2：利用toString() 转换成字符串`var str = num.toString();``console.log(str, typeof str);` // 输出结果：3.14 string
   * 方式 3：利用String() 转换成字符串`var str = String(num);``console.log(str, typeof str);` // 输出结果：3.14 string

2. 转换为数值型

   * 方式 1：使用parseInt() 将字符串转为整数:`console.log(parseInt('78'));` // 输出结果：78
   * 方式 2：使用parseFloat() 将字符串转为浮点数:`console.log(parseFloat('3.94'));` // 输出结果：3.94
   * 方式 3：使用Number() 将字符串转为数字型:`console.log(Number('3.94'));` // 输出结果：3.94
   * 方式 4：利用算术运算符（-、*、/）隐式转换:`console.log('12' - 1);` // 输出结果：11

|     待转数据     | Number()和隐式转换 |   parseInt()   |  parseFloat()  |
| :--------------: | :----------------: | :------------: | :------------: |
|   纯数字字符串   |   转成对应的数字   | 转成对应的数字 | 转成对应的数字 |
|     空字符串     |         0          |      NaN       |      NaN       |
| 数字开头的字符串 |        NaN         | 转成开头的数字 | 转成开头的数字 |
| 非数字开头字符串 |        NaN         |      NaN       |      NaN       |
|       null       |         0          |      NaN       |      NaN       |
|    undefined     |        NaN         |      NaN       |      NaN       |
|      false       |         0          |      NaN       |      NaN       |
|       true       |         1          |      NaN       |      NaN       |

### 运算符

1. 算术运算符
    +      `+`加、`−`减、`*`乘、`/`除、`%`取余数（取模)例：7 % 5  2    
2. 递增和递减运算符
   * 使用递增（++）、递减（−−）运算符可以快速地对变量的值进行递增和递减操作，它属于一元运算符，只对一个表达式进行操作;
3. 比较运算符:结果为`false`,`true`
   * `>`大于、`<`小于、`>=`大于或等于、`<=`小于或等于`==`等于、`!=`不等于、`===`全等、`!==`不全等
4. 逻辑运算符
   * `& &` 与 `a & & b`:a和 b 都为 true，结果为 true，否则为 false
   * `||` 或 `a || b`:a和 b 中至少有一个为 true，则结果为 true，否则为 false
   * `!` 非 `!a`:若 a为 false，结果为 true，否则相反
5. 赋值运算符
   * `=` 赋值a = 3;结果：a = 3
   * `+=` 加并赋值a = 3; a += 2;结果：a = 5
   * `−=` 减并赋值a = 3; a −= 2;结果：a = 1
   * `*=` 乘并赋值a = 3; a *= 2;结果：a = 6
   * `/=` 除并赋值a = 3; a /= 2;结果：a = 1.5
   * `%=` 求模并赋值a = 3; a % = 2;结果：a = 1
   * `+=` 连接并赋值a = 'abc'; a += 'def';结果：a = 'abcdef'
   * `<<=` 左移位并赋值a = 9; a <<= 2;结果：a = 36
   * `>>=` 右移位并赋值a = -9; a >>= 2;结果：a = -3
   * `>>>=` 无符号右移位并赋值a = 9; a >>>= 2;结果：a = 2
   * `&=` 按位“与”并赋值a = 3; a & = 9;结果：a = 1
   * `^=` 按位“异或”并赋值a = 3; a ^= 9;结果：a = 10
   * `=` 按位“或”并赋值a = 3; a结果：a = 9;
6. 三元运算符
   * 如果为 true，则返回表达式 1 的执行结果 ；如果条件表达式的值为 false，则返回表达式 2 的执行结果。

$$
条件表达式 ? 表达式1 : 表达式 2
$$

### 结构语句

1. 选择结构

   1. if语句

      `if ( 条件表达式 ) {// 代码段}`

   2. if…else 语句

      `if ( 条件表达式 ) {// 代码段1} else {// 代码段2}`

   3. if…else if 语句

      `if ( 条件表达式 1 ) {// 代码段 1} else if ( 条件表达式 2 ) {// 代码段 2}...else if ( 条件表达式 n ) {// 代码段 n} else {// 代码段 n+1}`

   4. switch 语句

      `switch ( 表达式 ) {case 值 1；代码段 1;break;case 值 2；代码段 2;break;...default:代码段 n;}`

2. 循环结构

   1. for 语句

      `for (初始化变量; 条件表达式; 操作表达式 ) {// 循环体}`

   2. while 语句:while语句可以在条件表达式为 true的前提下，循环执行指定的一段代码，直到条件表达式为 false时结束

      `while ( 条件表达式) {// 循环体}`

   3. do…while 语句:do…while语句的功能和 while语句类似，其区别在于，do…while会无条件地执行一次循环体中的代码，然后再判断条件，根据条件决定是否循环执行；

      `do {// 循环体} while ( 条件表达式);`

3. 关键字

   1. continue 关键字：continue关键字可以在 for、while以及 do…while循环体中使用，它用来立即跳出本次循环，也就是跳过了 continue后面的代码，继续下一次循环。
   2. break 关键字：break 关键字可以用在 switch 语句和循环语句中，在循环语句中使用时，其作用是立即跳出整个循环，也就是将循环结束。

###　数组

数组（Array）是一种复杂的数据类型，它属于 Object （对象）类型

1. 创建数组
   * 使用 new Array() 创建数组
     * `var arr1 = new Array();` // 空数组
     * `var arr2 = new Array(' 苹果 ', '橘子 ', '香蕉 ', '桃子 ');` // 含有 4个元素
   * 使用字面量来创建数组
     * `var arr1 = [];` // 空数组
     * `var arr2 = [' 苹果 ', '橘子 ', '香蕉 ', '桃子 '];` // 含有 4个元素
   * 在数组中保存各种常见的数据类型
     * `var arr1 = [123, 'abc', true, null, undefined];`
   * 在数组中保存数组
     * `var arr2 = [1, [21, 22], 3];`
   
2. 访问数组元素:==在数组中，每个元素都有索引（或称为下标），数组中的元素使用索引来进行访问。数组中的索引是一个数字，从 0 开始==

   ```mermaid
   graph TB
   A(var arr)
   Q(=)
   B[苹果]
   C[橘子]
   D[香蕉]
   E[桃子]
   AA(索引)
   QQ(:)
   BB[0]
   CC[1]
   DD[2]
   EE[3]
   A---AA
   Q---QQ
   B-->BB
   C-->CC
   D-->DD
   E-->EE
   
   ```
   
3. 数组元素操作:修改数组长度使用“数组名 .length”可以获取或修改数组的长度。

4. 冒泡排序不断比较数组中相邻两个元素的值，较小或较大的元素前移。
   
   ```
   var arr = [10, 7, 5, 27, 98, 31];
       for (var i = 1; i < arr.length; i++) { // 控制需要比较的轮数
           for (var j = 0; j < arr.length - i; j++) {// 控制参与比较的元素
                if (arr[j] > arr[j + 1]) { // 比较相邻的两个元素
                    var temp = arr[j + 1];
                    arr[j + 1] = arr[j];
                    arr[j] = temp;
                }}}
   console.log(arr); // 输出结果 ：5,7,10,27,31,98
   ```
   
5. 插入排序:插入排序是冒泡排序的优化，是一种直观的简单排序算法。它的实现原理是，通过构建有序数组元素的存储，对未排序的数组元素，在已排序的数组中从最后一个元素向第一个元素遍历，找到相应位置并插入。其中，待排序数组的第 1 个元素会被看作是一个有序的数组，从第 2 个至最后一个元素会被看作是一个无序数组。按照从小到大的顺序完成插入排序

   ```
   ar arr = [10, 8, 100, 31, 87, 70, 1, 88];
   // 按照从小到大的顺序排列，先遍历无序数组下标
   for (var i = 1; i < arr.length; i++) {
   // 遍历并比较一个无序数组元素与所有有序数组元素
       for (var j = i; j > 0; j--) {
           if (arr[j - 1] > arr[j]) {
               var temp = arr[j - 1];
               arr[j - 1] = arr[j];
               arr[j] = temp;
           }}}
    console.log(arr); // 输出结果 ：1,8,10,31,70,87,88,100　
   ```

#### 二维数组

1. 只需将数组元素设置为数组即可
   * 使用 Array创建数组
     * `var info = new Array(new Array('Tom', 13, 155),new Array('Lucy', 11, 152));`
     * `console.log(info[0]); // 输出结果：(3) ["Tom", 13, 155];console.log(info[0][0]); // 输出结果：Tom`
   * 使用 "[]"创建数组
     * `var nums = [[1, 2], [3, 4]];`
     * `console.log(nums[0]); // 输出结果：(2) [1, 2];console.log(nums[1][0]); // 输出结果：3`

2. 在实际开发中，还经常通过为空数组添加元素的方式来创建多维数组。
   * `var arr = [];` // 创建一维空数组
     `for (var i = 0 ; i < 3; i++) {arr[i] = [];` // 将当前元素设置为数组`arr[i][0] = i; `// 为二维数组元素赋值}

#### 二维数组转置

1. 二维数组的转置指的是将二维数组横向元素保存为纵向元素

   $$
   \textcolor{red}{转置前arr   \qquad\qquad\qquad\qquad 转置后arr}\\
   [\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad[\\
   ['a','b','c']\qquad\qquad\qquad\qquad\, ['a','d','g','j']\\
   ['d','e','f']\qquad\qquad\qquad\qquad['b','e','h','k']\\
   ['g','h','i']\qquad\qquad\qquad\qquad\, \ ['c','g','i','l']\\
   ['j','k','l']\qquad\qquad\qquad\qquad\qquad\qquad\qquad] \\
   ]\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad
   $$
   
2. 可以得出二维数组转置的公式为 res\[i][j] = arr\[j][i]，且 res数组的长度等于 arr元素（如 arr[0]）的长度，res元素（如 res[0]）的长度等于 arr数组的长度。

   * ```
     var arr = [['a', 'b', 'c'], ['d', 'e', 'f'], ['g', 'h', 'i'], ['j', 'k', 'l']];
     var res = [];
     for (var i = 0; i < arr[0].length; i++) {
         res[i] = [];
         for(var j = 0; j < arr.length; j++) {
             res[i][j] = arr[j][i]; // 为二维数组赋值
         }
     }
     console.log(res);
     ```

## 函数

函数在使用时分为两步，声明函数和调用函数，声明函数的基本语法如下。function 是声明函数的关键字，必须全部使用小写字母。

### function

Function：函数（方法）对象

1. 创建：

   1. `var fun = new Function(形式参数列表，方法体);`

   2. `fpnction 方法名称(形式参数列表){`

      ​      `方法体`

      `}`

   3. `var 方法名 = function(形式参数列表){`

      ​     `方法体`

      `}`

2. 方法：

3. 属性：

   length:代表形参的个数寺点：

4. 特点：

   1. 方法定义是,形参的类型不用写,返回值类型也不写。
   2. 方法是一个对象,如果定义名称相同的方法,会覆盖
   3. 在J5中,方法的调用只与方法的名称有关,和参数列表无关
   4. 在方法声明中有一个隐藏的内置对象(数组) , arguments,封装所有的实际参数

5. 调用：

   1. 方法名称（实际参数列表）；
   1. 当函数声明后，里面的代码不会执行，只有调用函数的时候才会执行。调用函数的语法为“函数名 ()”。

#### 函数的参数

1. 函数的参数

   * 形参:在声明函数时，可以在函数名称后面的小括号中添加一些参数，这些参数被称为形参。
   * `function 函数名(形参 1, 形参 2, …) { // 函数声明的小括号里的是形参// 函数体代码}`
   * 实参:当函数调用的时候，同样也需要传递相应的参数，这些参数称为实参。
   * `函数名 (实参 1, 实参 2, …); // 函数调用的小括号里的是实参`

2. 函数参数的数量

   * 允许函数的形参和实参个数不同
     * 当实参数量多于形参数量时，函数可以正常执行，多余的实参由于没有形参接收，会被忽略，除非用其他方式（如后面学到的 argum ents）才能获得多余的实参。
     * `function getSum(num1, num2) {console.log(num1, num2);}getSum(1, 2, 3);` // 实参数量大于形参数量，输出结果：1 2
     * 当实参数量小于形参数量时，多出来的形参类似于一个已声明未赋值的变量，其值为 undefined。
     * `getSum(1);` // 实参数量小于形参数量，输出结果：1 undefined

3. 函数的返回值:函数的返回值是通过 return 语句来实现的

4. 函数表达式

   * 函数表达式是将声明的函数赋值给一个变量，通过变量完成函数的调用和参数的传递。
   * 函数表达式与函数声明的定义方式几乎相同，不同的是函数表达式的定义必须在调用前，而函数声明的方式则不限制声明与调用的顺序。
   * `var sum = function(num1, num2) {` // 函数表达式`return num1 + num2;};`
   * `console.log(sum(1, 2));` // 调用函数，输出结果：3

5. 回调函数

   * 回调函数指的就是一个函数 A 作为参数传递给一个函数 B，然后在 B 的函数体内调用函数 A。此时，我们称函数 A 为回调函数。其中，匿名函数常用作函数的参数传递，实现回调函数

   * ```
     function cal(num1, num2, fn) {
         return fn(num1, num2);
     }
     console.log(cal(45, 55, function (a, b) {
         return a + b;
     }));
     console.log(cal(10, 20, function (a, b) {
         return a * b;
     }));
     ```

6. 递归调用

   * 递归调用是函数嵌套调用中一种特殊的调用。它指的是一个函数在其函数体内调用自身的过程，这种函数称为递归函数。需要注意的是，递归函数只可在特定的情况下使用，如计算阶乘。

   * ```
     function factorial(n) { // 定义回调函数
         if (n == 1) {
             return 1; // 递归出口
         }
         return n * factorial(n - 1);
     }
     var n = prompt(' 求 n的阶乘\n n是大于等于 1的正整数，如 2表示求 2!。');
     n = parseInt(n);//将字符串转为整数
     if (isNaN(n)) {
         console.log(' 输入的n值不合法 ');
     } else {
         console.log(n + ' 的阶乘为 ：' + factorial(n));
     }
     ```
     
     ```mermaid
     graph LR
     subgraph one
     A[第一次递归n=4 return 4 * factorial 4-1]
     B[第二次递归n=3 return 3 * factorial 3-1]
     C[第三次递归n=2 return 2 * factorial 2-1]
     D[第四次递归n=1]
     end
     subgraph two
     E[return 24]
     Q[factorial 4] 
     F[return 6]
     G[return 2]
     H[return 1]
     end
     A-->B-->C-->D-->H-->C-->G-->B-->F-->A-->E-->Q-->A
     ```
     
     

![s](D:\笔记\typoratuxiang\JavaScript\JavaScript递归函数.PNG)

7. 作用域的分类

   1. 全局变量 ：不在任何函数内声明的变量（显式定义）或在函数内省略 var声明的变量（隐式定义）都称为全局变量，它在同一个页面文件中的所有脚本内都可以使用。
   2. 局部变量 ：在函数体内利用 var关键字定义的变量称为局部变量，它仅在该函数体内有效。
   3. 块级变量 ：ES 6 提供的 let关键字声明的变量称为块级变量，仅在“{}”中间有效,如 if、for或 while语句等。

8. 作用域链：当在一个函数内部声明另一个函数时，就会出现函数嵌套的效果。当函数嵌套时，内层函数只能在外层函数作用域内执行，在内层函数执行的过程中，若需要引入某个变量，首先会在当前作用域中寻找，若未找到，则继续向上一层级的作用域中寻找，直到全局作用域。我们称这种链式的查询关系为作用域链。

9. 闭包函数

   * 实现外层函数调用内层函数；所谓“闭包”指的就是有权访问另一函数作用域内变量（局部变量）的函数。它最主要的用途是以下两点。

     1. 可以在函数外部读取函数内部的变量。

     2. 可以让变量的值始终保持在内存中。

     3. 常见的闭包创建方式就是在一个函数内部创建另一个函数，通过另一个函数访问这个函数的局部变量。

        ```
        function fn() {
            var times = 0;
            var c = function () {
                return ++times;
            };
            return c;
        }
        var count = fn(); // 保存 fn()返回的函数，此时 count就是一个闭包
        // 访问测试
        console.log(count()); // 输出结果：1
        console.log(count()); // 输出结果：2
        console.log(count()); // 输出结果：3
        console.log(count()); // 输出结果：4
        console.log(count()); // 输出结果：5
        ```

10. 预解析:JavaScript代码是由浏览器中的 JavaScript解析器来执行的，JavaScript解析器在运行JavaScript代码的时候会进行预解析，也就是提前对代码中的 var变量声明和 function 函数声明进行解析，然后再去执行其他的代码。函数表达式不会被预解析

## 对象

==在 JavaScript中，对象是一种数据类型，它是由属性和方法组成的一个集合。属性是指事物的特征，方法是指事物的行为。==

1. 利用字面量创建对象

   * 在 JavaScript中，对象的字面量就是用花括号“{ }”来包裹对象中的成员，每个成员使用“key: value”的形式来保存，key表示属性名或方法名，value表示对应的值。多个对象成员之间用“,”隔开。

     ```
     var obj = {};// 创建一个空对象
     var stu1 = {// 创建一个学生对象
         name: ' 小明 ', // name 属性
         age: 18, // age 属性
         sex: ' 男 ', // sex 属性
         sayHello: function() { 'sayHello 方法'console.log('Hello');}};
     ```

2. 访问对象的属性和方法

   * 访问对象的属性（语法1）`console.log(stu1.name);` // 输出结果：小明
   * 访问对象的属性（语法2）`console.log(stu1['age']);` // 输出结果：18
   * 调用对象的方法（语法1）`stu1.sayHello();` // 输出结果：Hello
   * 调用对象的方法（语法2）`stu1['sayHello']();` // 输出结果：Hello

3. 利用 new Object 创建对象

   * 数组是一种特殊的对象，如果要创建一个普通的对象，则使用 new Object进行创建。

     ```
     var obj = new Object(); // 创建了一个空对象
     obj.name = ' 小明 '; // 创建对象后，为对象添加成员
     obj.age = 18;
     obj.sex = ' 男 ';
     obj.sayHello = function() {
     console.log('Hello');
     };
     ```

4. 利用构造函数创建对象

   * 语法`new 构造函数名()`在小括号中可以传递参数给构造函数，如果没有参数， 小括号可以省略。

   * `new Object()`就是一种使用构造函数创建对象的方式，Object就是构造函数的名称，

   * 但这种方式创建出来的是一个空对象。如果我们想要创建的是一些具有相同特征的对象，则可以自己写一个构造函数。

     ```
     // 编写构造函数
     function 构造函数名 () {
      this. 属性 = 属性 ;
      this. 方法 = function() {'方法体'};}
     // 使用构造函数创建对象
     var obj = new 构造函数名 ();
     ```

5. 构造函数中的 this 表示新创建出来的对象，在构造函数中可以通过 this 来为新创建出来的对象添加成员。需要注意的是，构造函数的名称推荐首字母大写。

   * 抽象 ：将一类对象的共同特征提取出来，编写成一个构造函数（类）的过程，称为抽象。 

   * 实例化 ：利用构造函数（类）创建对象的过程，称为实例化。 

   * 实例 ：如果 stu1 对象是由 Student 构造函数创建出来的，则 stu1 对象称为 Student 构造 函数的实例（或称为实例对象）。

   * static ：静态，静态成员， 是指构造函数本身就有的属性和方法，不需要创建实例对象就能使用。

   * ```javascript
     function Student() {}
     Student.school = 'X 大学 '; // 添加静态属性 school
     Student.sayHello = function() {console.log('Hello');};
     // 添加静态方法 sayHello
     console.log(Student.school); // 输出结果 ：X 大学
     Student.sayHello(); // 输出结果 ：Hello
     ```

### 遍历对象的属性和方法

1. 使用 for…in 语法可以遍历对象中的所有属性和方法
   * 准备一个待遍历的对象`var obj = { name: ' 小明 ', age: 18, sex: ' 男 ' };`
   * 遍历 obj 对象`for (var k in obj) {` // 通过 k 可以获取遍历过程中的属性名或方法名`console.log(k);` // 依次输出 ：name、age、sex`console.log(obj[k]);` // 依次输出 ：小明、18、男
   * 当需要判断一个对象中的某个成员是否存在时，可以使用 in 运算符。
     * `var obj = {name: 'Tom', age: 16};console.log('age' in obj);` // 输出结果 ：true`console.log('gender' in obj);` // 输出结果 ：false
     * 当对象的成员存在时返回 true，不存在时返回 false。
2. 在通过文档学习某个方法的使用时，可以分为 4 个步骤
   * 查阅方法的功能。
   * 查看参数的意义和类型。使用“[]”包裹的参数表示可选参数，可以省略。
   * 查看返回值的意义和类型。
   * 通过示例代码进行测试。

### Math对象

1. Math 对象用来对数字进行与数学相关的运算，该对象不是构造函数，不需要实例化对象， 可以直接使用其静态属性和静态方法。

   * `PI`:获取圆周率，结果为 3.141592653589793 
     * `Math.PI;` // 获取圆周率
   * `abs(x)`:获取 x 的绝对值，可传入普通数值或是用字符串表示的数值
     * `Math.abs(-25);` // 获取绝对值，返回结果 ：25
   * `max([value1[,value2, ...]])`:获取所有参数中的最大值
     * `Math.max(5, 7, 9, 8);` // 获取最大值，返回结果 ：9
   * `min([value1[,value2, ...]])`:获取所有参数中的最小值
     * `Math.min(6, 2, 5, 3);` // 获取最小值，返回结果 ：2
   * `pow(base, exponent)`:获取基数（base）的指数（exponent）次幂，即 baseexponent
     * `Math.pow(2, 4);` // 获取 2 的 4 次幂，返回结果 ：16
   * `sqrt(x)`:获取 x 的平方根
     * `Math.sqrt(9);` // 获取 9 的平方根，返回结果为 ：3
   * `ceil(x)`:获取大于或等于 x 的最小整数，即向上取整
     * `Math.ceil(1.1);` // 向上取整，返回结果 ：2
   * floor(x): 获取小于或等于 x 的最大整数，即向下取整
     * `Math.floor(1.1);` // 向下取整，返回结果 ：1
   * `round(x)`:获取 x 的四舍五入后的整数值
     * `Math.round(1.9);` // 四舍五入，返回结果 ：2
   * `random()`:获取大于或等于 0.0 且小于 1.0 的随机值
     * `Math.random();`

2. 生成指定范围的随机数

   * `Math.random()`返回的结果0 ～ 1（不包括 1）。任意范围内的随机数，公式为“Math.random() * (max - min) + min”，表示生成大于或等于 min 且小于 max 的随机值。

   * 因为结果是浮点数，当需要获取整数结果时，可以搭配 Math.floor() 来实现。获取 1 ～ 3 范围内的随机整数，返回结果可能是 1、2 或 3。

     * `function getRandom(min, max) {return Math.floor(Math.random() * (max - min + 1) + min);}console.log(getRandom(1, 3)); // 最小值 1，最大值 3`

   * 可以使用`Math.floor(Math.random() * (max + 1))`表示生成0到max之间的随机整数,使用`Math.floor(Math.random()*(max+1)+1)`表示生成1到max之间的随机整数。

   * ```
     var arr = ['apple', 'banana', 'orange', 'pear'];// 调用前面编写的 getRandom() 函数获取随机数
     console.log(arr[getRandom(0, arr.length - 1)]);
     ```

### 日期对象Date

1. 日期对象的使用

   * 日期对象需要使用`new Date()`实例化对象才能使用，Date() 是日期对象的构造函数。在创建日期对象时，可以为 Date()构造函数传入一些参数，来表示具体的日期，其创建方式如下。

   * 方式 1 ：没有参数，使用当前系统的当前时间作为对象保存的时间

     * `var date1 = new Date();console.log(date1);` 输出结果 ：Wed Oct 16 2019 10:57:56 GMT+0800 ( 中国标准时间 )

     ```javascript
     var date1 = new Date();//输出结果 ：Wed Oct 16 2019 10:57:56 GMT+0800 ( 中国标准时间 )
     console.log(date1); 
     ```

   * 方式 2 ：传入年、月、日、时、分、秒（月的范围是 0 ～ 11，即真实月份 -1）

     ```javascript
     var date2 = new Date(2019, 10, 16, 10, 57, 56);// 输出结果 ：Sat Nov 16 2019 10:57:56 GMT+0800 ( 中国标准时间 )
     console.log(date2); 
     ```

   * 方式 3 ：用字符串表示日期和时间

     ```javascript
     var date3 = new Date('2019-10-16 10:57:56');// 输出结果 ：Wed Oct 16 2019 10:57:56 GMT+0800 ( 中国标准时间 )
     console.log(date3);
     ```

2. Date 对象的常用 get 方法

   * | 方法              | 作用                                                         |
     | ----------------- | ------------------------------------------------------------ |
     | getFullYear()     | 获取表示年份的 4 位数字，如 2020                             |
     | getMonth()        | 获取月份，范围为 0 ～ 11（0 表示一月，1 表示二月，依次类推） |
     | getDate()         | 获取月份中的某一天，范围 1 ～ 31                             |
     | getDay()          | 获取星期，范围为 0 ～ 6（0 表示星期日，1 表示星期一，依次类推） |
     | getHours()        | 获取小时数，范围为 0 ～ 23                                   |
     | getMinutes()      | 获取分钟数，范围为 0 ～ 59                                   |
     | getSeconds()      | 获取秒数，范围为 0 ～ 59                                     |
     | getMilliseconds() | 获取毫秒数，范围为 0 ～ 999                                  |
     | getTime()         | 获取从 1970-01-01 00:00:00 距离 Date 对象所代表时间的毫秒数  |

3. Date 对象的常用 set 方法

   * | 方法                   | 作用                                       |
     | ---------------------- | ------------------------------------------ |
     | setFullYear(value)     | 设置年份                                   |
     | setMonth(value)        | 设置月份                                   |
     | setDate(value)         | 设置月份中的某一天                         |
     | setHours(value)        | 设置小时数                                 |
     | setMinutes(value)      | 设置分钟数                                 |
     | setSeconds(value)      | 设置秒数                                   |
     | setMilliseconds(value) | 设置毫秒数                                 |
     | setTime(value) 通过从  | 1970-01-01 00:00:00 计时的毫秒数来设置时间 |

### Array数组对象

1. 创建：
   1. `var arr = new Array(元素列表);`
   2. `var arr = new Array(默认长度)；`
   3. `var arr =[元素列表];`
2. 方法：
   1. join(参数)：将数组中的元素按照指定的分隔符拼接为字符串
   2. qush() 向数组的末尾添加一个或更多元素,并返回新的长度。
3. 属性：：
   1. length:数组的长度
4. 特点：
   1. JS中,数组元素的类型可变的。
   2. JS中，数组长度可变的。

* 使用 new Array 或字面量“[ ]”来创建，在创建以后，就可以调用数组对象提供的一些方法来实现对数组的操作了，如添加或删除数组元素、数组排序、 数组索引等。

1. 数组类型检测

   * 数组类型检测有两种常用的方式，分别是使用

   * `var arr = [];var obj = {};`

     * instanceof 运算符

       ```javascript
       console.log(arr instanceof Array); // 输出结果 ：true
       console.log(obj instanceof Array); // 输出结果 ：false
       ```

     * Array.isArray() 方法。

       ```javascript
       console.log(Array.isArray(arr)); // 输出结果 ：true
       console.log(Array.isArray(obj)); // 输出结果 ：false
       ```

2. 添加或删除数组元素

   * 需要注意的是，push() 和 unshift() 方法的返回值是新数组的长度，而 pop() 和 shift() 方法返回的是移出的数组元素。
     * `var arr = ['Rose', 'Lily'];console.log(' 原数组 ：' + arr);`
   * push( 参数 1…):数组末尾添加一个或多个元素，会修改原数组;返回数组的新长度
     * `var len = arr.push('Tulip', 'Jasmine');console.log(' 在末尾添加元素后长度变为 ：' + len + ' - 添加后数组 ：' + arr);`
   * unshift( 参数 1…):数组开头添加一个或多个元素，会修改原数组;返回数组的新长度
     * `len = arr.unshift('Balsam', 'sunflower');console.log(' 在开头添加元素后长度变为 ：' + len + ' - 添加后数组 ：' + arr);`
   * pop():删除数组的最后一个元素，若是空数组则返回`undefined`会修改原数组;返回删除的元素的值
     * `var last = arr.pop();console.log(' 在末尾移出元素 ：' + last + ' - 移出后数组 ：' + arr);`
   * shift():删除数组的第一个元素，若是空数组则返回`undefined`会修改原数组;返回第一个元素的值
     * `var first = arr.shift();console.log(' 在开头移出元素 ：' + first + ' - 移出后数组 ：' + arr);`

3. 数组排序

   * `reverse()`颠倒数组中元素的位置，该方法会改变原数组

   * `sort()`对数组的元素进行排序，该方法会改变原数组

   * reverse() 和 sort() 方法的返回值是新数组的长度。

     ```javascript
     // 反转数组
     var arr = ['red', 'green', 'blue'];
     arr.reverse();
     console.log(arr); // 输出结果 ：(3) ["blue", "green", "red"]
     // 数组排序
     var arr1 = [13, 4, 77, 1, 7];
     arr1.sort(function(a, b) {
     return b - a; // 按降序的顺序排列
     });
     console.log(arr1); // 输出结果 ：(5) [77, 13, 7, 4, 1]
     ```

4. 数组索引:默认都是从指定数组索引的位置开始检索，并且检索方式与运算符“===” 相同，即只有全等时才会返回比较成功的结果.

   * 若要查找指定的元素在数组中的位置，则可以利用 Array 对象提供的检索方法
   
   * `indexOf()`返回在数组中可以找到给定值的第一个索引，如果不存在，则返回 -1
   
   * `lastIndexOf()`返回指定元素在数组中的最后一个的索引，如果不存在则返回 -1
   
     ```
      var arr = ['red', 'green', 'blue', 'pink', 'blue'];
      console.log(arr.indexOf('blue')); // 输出结果 ：2
      console.log(arr.lastIndexOf('blue')); // 输出结果 ：4
     ```
   
5. 数组转换为字符串

   * `join('分隔符')`:将数组的所有元素连接到一个字符串中

     ```
     console.log(arr.join()); // 输出结果 ：a,b,c
     console.log(arr.join('')); // 输出结果 ：abc
     console.log(arr.join('-')); // 输出结果 ：a-b-c
     ```

   * `toString()`:把数组转换为字符串，逗号分隔每一项

     ```
     var arr = ['a', 'b', 'c'];
     console.log(arr.toString()); // 输出结果 ：a,b,c\
     ```

6. `fill()` : 用一个固定值填充数组中指定下标范围内的全部元素

7. `splice()` : 数组删除，参数为 splice( 第几个开始 , 要删除个数 )，返回被删除项目的新数组

8. `slice()` : 数组截取，参数为 slice(begin, end)，返回被截取项目的新数组

9. `concat()` : 连接两个或多个数组，不影响原数组，返回一个新数组

### 字符串对象

1. 字符串对象的使用

   * 字符串对象使用 new String() 来创建，在 String 构造函数中传入字符串，就会在返回的字符串对象中保存这个字符串。

     ```
     var str = new String('apple'); // 创建字符串对象
     console.log(str); // 输出结果 ：String {"apple"}
     console.log(str.length); // 获取字符串长度，输出结果 ：5
     ```

2. 基本包装类型包括 String、Number 和 Boolean，用来把基本数据类型包装成为复杂数据类型，从而使基本数据类型也有了属性和方法。

   * 虽然 JavaScript 基本包装类型的机制可以使普通变量也能像对象一样访 问属性和方法，但它们并不属于对象类型。

   * 使用 new String() 返回的 obj 是一个对象，但是普通的字符串变量 并不是一个对象，它只是一个字符串类型的数据。

     ```
     var obj = new String('Hello');
     console.log(typeof obj); // 输出结果 ：object
     console.log(obj instanceof String); // 输出结果 ：true
     var str = 'Hello';
     console.log(typeof str); // 输出结果 ：string
     console.log(str instanceof String); // 输出结果 ：false
     ```

3. 字符返回位置:字符串对象用于检索元素的属性和方法

   * indexOf(searchValue)  获取 searchValue 在字符串中首次出现的位置

   * lastIndexOf(searchValue)  获取 searchValue 在字符串中最后出现的位置

   * 位置从 0 开始计算，字符串第一个字符的位置是 0，第 2 个字 符为 1，以此类推，最后一个字符的位置是字符串的长度减 1。

     ```
     var str = 'HelloWorld';
     str.indexOf('o'); // 获取 "o" 在字符串中首次出现的位置，返回结果 ：4
     str.lastIndexOf('o'); // 获取 "o" 在字符串中最后出现的位置，返回结果 ：6
     ```

4. 字符串对象用于获取某一个字符的方法

   * charAt(index)  获取 index 位置的字符，位置从 0 开始计算

   * charCodeAt(index)  获取 index 位置的字符的 ASCII 码

   * str[index]  获取指定位置处的字符（HTML5 新增）

     ```
     var str = 'Apple';
     console.log(str.charAt(3)); // 输出结果 ：1
     console.log(str.charCodeAt(0)); // 输出结果 ：65（字符 A 的 ASCII 码为 65）
     console.log(str[0]); // 输出结果 ：A
     ```

5. 字符串操作方法:字符串对象用于截取、连接和替换字符串的方法

   * | 成员                       | 作用                                                         |
     | -------------------------- | ------------------------------------------------------------ |
     | concat(str1, str2, str3…)  | 连接多个字符串                                               |
     | slice(start,[ end])        | 截取从 start 位置到 end 位置之间的一个子字符串               |
     | substring(start[, end])    | 截取从 start 位置到 end 位置之间的一个子字符串，基本和 slice 相同，但是不接收负值 |
     | substr(start[, length])    | 截取从 start 位置开始到 length 长度的子字符串                |
     | toLowerCase()              | 获取字符串的小写形式                                         |
     | toUpperCase()              | 获取字符串的大写形式                                         |
     | split([separator[, limit]) | 使用 separator 分隔符将字符串分隔成数组，limit 用于限制数量  |
     | replace(str1, str2)        | 使用 str2 替换字符串中的 str1，返回替换结果，只会替换第一个字符 |

     ```
     var str = 'HelloWorld';
     str.concat('!'); 　　// 在字符串末尾拼接字符，结果 ：HelloWorld!
     str.slice(1, 3); 　　// 截取从位置 1 开始到位置 3 范围内的内容，结果 ：el
     str.substring(5); 　　// 截取从位置 5 开始到最后的内容，结果 ：World
     str.substring(5, 7); 　　// 截取从位置 5 开始到位置 7 范围内的内容，结果 ：Wo
     str.substr(5); // 截取从位置 5 开始到字符串结尾的内容，结果 ：World
     str.substring(5, 7); // 截取从位置 5 开始到位置 7 范围内的内容，结果 ：Wo
     str.toLowerCase(); // 将字符串转换为小写，结果 ：helloworld
     str.toUpperCase(); // 将字符串转换为大写，结果 ：HELLOWORLD
     str.split('l'); // 使用 "l" 切割字符串，结果 ：["He", "", "oWor", "d"]
     str.split('l', 3); // 限制最多切割 3 次，结果 ：["He", "", "oWor"]
     str.replace('World', '!'); // 替换字符串，结果 ："Hello!"
     ```

6. 值类型和引用类型

   * 基本数据类型（如字符串型、数字型、布尔型、undefined、null）又称 为值类型

   * 复杂数据类型(对象)又称为引用类型。

   * 引用类型的特点是，变量中保存的仅仅 是一个引用的地址，当对变量进行赋值时，并不是将对象复制了一份，而是将两个变量指向 了同一个对象的引用。

   * obj1 和 obj2 两个变量引用了同一个对象，此时，无论是使用 obj1 操作对象还是使用 obj2 操作对象，实际操作的都是同一个对象

     ```
     // 创建一个对象，并通过变量 obj1 保存对象的引用
     var obj1 = { name: ' 小明 ', age: 18 };
     // 此时并没有复制对象，而是 obj2 和 obj1 两个变量引用了同一个对象
     var obj2 = obj1;
     // 比较两个变量是否引用同一个对象
     console.log(obj2 === obj1); // 输出结果 ：true
     // 通过 obj2 修改对象的属性
     obj2.name = ' 小红 ';
     // 通过 obj1 访问对象的 name 属性
     console.log(obj1.name); // 输出结果 ：小红
     ```

   * 当 obj1 和 obj2 两个变量指向了同一个对象后，如果给其中一个变量（如 obj1）重新赋值为其他对象，或者重新 赋值为其他值，则 obj1 将不再引用原来的对象，但 obj2 仍 然在引用原来的对象

     ```
     var obj1 = { name: ' 小明 ', age: 18 };
     var obj2 = obj1;
     // obj1 指向了一个新创建的对象
     obj1 = { name: ' 小红 ', age: 17 };
     // obj2 仍然指向原来的对象
     console.log(obj2.name); // 输出结果 ：小明
     ```

   * 当引用类型的变量作为函数的参数来传递时，其效果和变量之间的赋值类似。如果在函数的参数中修改对象的属性或方法，则在函数外面通过引用这个对象的变量访问到的结果也是修改后的

   * 当调用 change() 函数后，在 change() 函数中修改了 obj.name 的值。修改后，在函数外面通过 stu 变量访问到的结果是修改后的值，说明变量 stu 和参数 obj 引用的是同一个对象。

     ```
     function change(obj) {
         obj.name = ' 小红 '; // 在函数内修改了对象的属性
     }
     var stu = { name: ' 小明 ', age: 18 };
     change(stu);
     console.log(stu.name); // 输出结果 ：小红
     ```

### Function对象

1. 创建Function对象的三种方式
   1. `var fun = new Function(形参列表，方法体)`
   2. `function fun1(a){alert(a)}`
   3. `var fun=function(a){alert(a)}`
2. 属性
   1. length：返回形参个数
3. 调用
   1. 方法名称（实参）
4. 特点
   1. 方法定义是，形参的类型不用写，返回值类型也不写。
   2. 方法是一个对象，如果定又名称相同的方法，会覆盖
   3. 在JS中，方法的调用只与方法的名称有关，和参数列表无关
   4. 在方法声明中有一个的内置对象（数组），arguments, 封装所有的实际参数

### RegExp正则表达式对象

1. 定义字符串组成规则

   #### 方括号

   方括号用于查找某个范围内的字符：

   | 表达式                                                       | 描述                                     |
   | :----------------------------------------------------------- | :--------------------------------------- |
   | [[abc\]](https://www.w3school.com.cn/jsref/jsref_regexp_charset.asp) | 查找括号之间的任何字符。                 |
   | [[^abc\]](https://www.w3school.com.cn/jsref/jsref_regexp_charset_not.asp) | 查找任何不在方括号之间的字符。           |
   | [[0-9\]](https://www.w3school.com.cn/jsref/jsref_regexp_0-9.asp) | 查找任何从 0 至 9 的数字。               |
   | [[^0-9\]](https://www.w3school.com.cn/jsref/jsref_regexp_not_0-9.asp) | 查找任何不在括号内的字符（任何非数字）。 |
   | [(x\|y)](https://www.w3school.com.cn/jsref/jsref_regexp_xy.asp) | 查找任何指定的选项。                     |

   #### 元字符

   元字符是具有特殊含义的字符：

   | 元字符                                                       | 描述                                                         |
   | :----------------------------------------------------------- | :----------------------------------------------------------- |
   | [.](https://www.w3school.com.cn/jsref/jsref_regexp_dot.asp)  | 查找单个字符，除了换行符或行终止符。                         |
   | [\w](https://www.w3school.com.cn/jsref/jsref_regexp_wordchar.asp) | 查找单词字符。                                               |
   | [\W](https://www.w3school.com.cn/jsref/jsref_regexp_wordchar_non.asp) | 查找非单词字符。                                             |
   | [\d](https://www.w3school.com.cn/jsref/jsref_regexp_digit.asp) | 查找数字。                                                   |
   | [\D](https://www.w3school.com.cn/jsref/jsref_regexp_digit_non.asp) | 查找非数字字符。                                             |
   | [\s](https://www.w3school.com.cn/jsref/jsref_regexp_whitespace.asp) | 查找空白字符。                                               |
   | [\S](https://www.w3school.com.cn/jsref/jsref_regexp_whitespace_non.asp) | 查找非空白字符。                                             |
   | [\b](https://www.w3school.com.cn/jsref/jsref_regexp_begin.asp) | 在单词的开头/结尾查找匹配项，开头如下：\bHI，结尾如下：HI\b。 |
   | [\B](https://www.w3school.com.cn/jsref/jsref_regexp_begin_not.asp) | 查找匹配项，但不在单词的开头/结尾处。                        |
   | [\0](https://www.w3school.com.cn/jsref/jsref_regexp_nul.asp) | 查找 NULL 字符。                                             |
   | [\n](https://www.w3school.com.cn/jsref/jsref_regexp_newline.asp) | 查找换行符。                                                 |
   | [\f](https://www.w3school.com.cn/jsref/jsref_regexp_formfeed.asp) | 查找换页符。                                                 |
   | [\r](https://www.w3school.com.cn/jsref/jsref_regexp_carriagereturn.asp) | 查找回车符。                                                 |
   | [\t](https://www.w3school.com.cn/jsref/jsref_regexp_tab.asp) | 查找制表符。                                                 |
   | [\v](https://www.w3school.com.cn/jsref/jsref_regexp_vtab.asp) | 查找垂直制表符。                                             |
   | [\xxx](https://www.w3school.com.cn/jsref/jsref_regexp_octal.asp) | 查找以八进制数 xxx 规定的字符。                              |
   | [\xdd](https://www.w3school.com.cn/jsref/jsref_regexp_hex.asp) | 查找以十六进制数 dd 规定的字符。                             |
   | [\uxxxx](https://www.w3school.com.cn/jsref/jsref_regexp_unicode_hex.asp) | 查找以十六进制数 xxxx 规定的 Unicode 字符。                  |

   #### 量词

   | 量词                                                         | 描述                                        |
   | :----------------------------------------------------------- | :------------------------------------------ |
   | [n+](https://www.w3school.com.cn/jsref/jsref_regexp_onemore.asp) | 匹配任何包含至少一个 n 的字符串。           |
   | [n*](https://www.w3school.com.cn/jsref/jsref_regexp_zeromore.asp) | 匹配任何包含零个或多个 n 的字符串。         |
   | [n?](https://www.w3school.com.cn/jsref/jsref_regexp_zeroone.asp) | 匹配任何包含零个或一个 n 的字符串。         |
   | [n{X}](https://www.w3school.com.cn/jsref/jsref_regexp_nx.asp) | 匹配包含 X 个 n 的序列的字符串。            |
   | [n{X,Y}](https://www.w3school.com.cn/jsref/jsref_regexp_nxy.asp) | 匹配包含 X 至 Y 个 n 的序列的字符串。       |
   | [n{X,}](https://www.w3school.com.cn/jsref/jsref_regexp_nxcomma.asp) | 匹配包含至少 X 个 n 的序列的字符串。        |
   | [n$](https://www.w3school.com.cn/jsref/jsref_regexp_ndollar.asp) | 匹配任何以 n 结尾的字符串。                 |
   | [^n](https://www.w3school.com.cn/jsref/jsref_regexp_ncaret.asp) | 匹配任何以 n 开头的字符串。                 |
   | [?=n](https://www.w3school.com.cn/jsref/jsref_regexp_nfollow.asp) | 匹配任何其后紧接指定字符串 n 的字符串。     |
   | [?!n](https://www.w3school.com.cn/jsref/jsref_regexp_nfollow_not.asp) | 匹配任何其后没有紧接指定字符串 n 的字符串。 |

1. 对象

   1. 创建

      * `var reg = new RegExp("正则表达式");`
      * `var reg = /^正则表达式$/;`
      * 开始`^`结束`$`符号

   2. 方法

      * text(参数)：验证字符串是否符合正常表达式定义的规范

      ```javascript
      var reg = /^\w{7}$/;
      var user = "zhangsan";
      alert(reg.test(user));
      ```

### Global对象

1. 特点：全局对象，这个Global这个对象中的方法不需要对象可以直接调用。方法名（）；

2. 方法：

   | 函数                                                         | 描述                                                         |
   | :----------------------------------------------------------- | :----------------------------------------------------------- |
   | [decodeURI()](https://www.w3school.com.cn/jsref/jsref_decodeuri.asp) | 解码 URI。                                                   |
   | [decodeURIComponent()](https://www.w3school.com.cn/jsref/jsref_decodeuricomponent.asp) | 解码 URI 组件。                                              |
   | [encodeURI()](https://www.w3school.com.cn/jsref/jsref_encodeuri.asp) | 对 URI 进行编码。                                            |
   | [encodeURIComponent()](https://www.w3school.com.cn/jsref/jsref_encodeuricomponent.asp) | 对 URI 组件进行编码。                                        |
   | [escape()](https://www.w3school.com.cn/jsref/jsref_escape.asp) | 在 1.5 版中已弃用。请使用 [encodeURI()](https://www.w3school.com.cn/jsref/jsref_encodeuri.asp) 或 [encodeURIComponent()](https://www.w3school.com.cn/jsref/jsref_encodeuricomponent.asp) 代替。 |
   | [eval()](https://www.w3school.com.cn/jsref/jsref_eval.asp)   | 将字符串并像脚本代码一样执行它。                             |
   | [isFinite()](https://www.w3school.com.cn/jsref/jsref_isfinite.asp) | 确定值是否是有限的合法数。                                   |
   | [isNaN()](https://www.w3school.com.cn/jsref/jsref_isnan.asp) | 确定值是否是非法数字。                                       |
   | [Number()](https://www.w3school.com.cn/jsref/jsref_number.asp) | 将对象的值转换为数字。                                       |
   | [parseFloat()](https://www.w3school.com.cn/jsref/jsref_parsefloat.asp) | 解析字符串并返回浮点数。                                     |
   | [parseInt()](https://www.w3school.com.cn/jsref/jsref_parseint.asp) | 解析字符串并返回整数。                                       |
   | [String()](https://www.w3school.com.cn/jsref/jsref_string.asp) | 将对象的值转换为字符串。                                     |
   | [unescape()](https://www.w3school.com.cn/jsref/jsref_unescape.asp) | 在 1.5 版中已弃用。请使用 [decodeURI()](https://www.w3school.com.cn/jsref/jsref_decodeuri.asp) 或 [decodeURIComponent()](https://www.w3school.com.cn/jsref/jsref_decodeuricomponent.asp) 代替。 |

## BOM

* 浏览器对象模型：将浏览器的各个组成部分封装成对象

* 对象

   * Window：窗口对象

      1. 创建

      2. 方法

         1. 弹出框

            * `alert()`：显示带有一段消息和一个确认按钮的警告框。

            * `confirm()`：显示带有一段消息以及确认按钮和取消按钮的对话框。
            * `prompt()`：显示可提示用户输入的对话框。

         2. 打开关闭

            * `open()`：打开一个新的浏览器窗口或查找一个已命名的窗口。
            * `close()`：关闭浏览器窗口。谁调用，关闭谁

         3. 定时器

            * `setTimeout()`：在指定的毫秒数后调用函数或计算表达式。
               * 参数：js代码，方法对象；毫秒值
               * 返回值：id
            * `clearTimeout()`：取消由 setTimeout() 方法设置的 timeout。
            * `setInterval()`：按照指定的周期（以毫秒计）来调用函数或计算表达式。
            * `clearInterval()`：取消由 setInterval() 设置的 timeout。

      3. 属性

         * 获取其他windows对象

      4. 特点

         * 不需要创建可以直接使用。`windows.方法名()`
         * 可以省略windows。`方法名()`

   * Navigator：浏览器对象

   * Screen：显示器屏幕对象

   * History：历史记录对象

   * Location：地址栏对象

      1. 创建
         * `Location.方法名()`
         * `方法名()`
      2. 属性
         * href：设置或返回完整的URL。
      3. 方法
         * `reload()`：重新加载当前窗口

## DOM

* 文档对象模型：将标记语言文档的各个组成部分，封装为对象。可以使用些对象，对标记文档进行 CRUD 的动态操作

* 功能：控制html文档的内容
  
  * 获取页面标签元素：`document.getElementById(id值)`通过id元素获取
  
* 操作Element对象
  1. 修改属性值，可以修改原标签有的所有属性值`document.getElementById(1).value="111";`、`<input id="1" type="text" value="123">`
  2. 修改标签体内容`document.getElementById(2).innerHTML="奶茶妹妹";`\.innerHTML内置对象
  
* DOM分为3个标准

  1. 核心DOM：针对任何结构化文档的标准模型

     * 对象

       * Document：文档对象

         1. 创建（获取）：在html中可以使用windows对象来获取

            * `windows.document`
            * `document`

         2. 方法

            * 获取Element对象：

              1. `getElementById()`：查找具有指定的唯一 ID 的元素。ID属性值唯一
              2. `getElementsByTagName()`：返回所有具有指定名称的元素节点。返回值是一个数组
              3. `getElementByClassName()`：根据Class属性值获取元素对象们。返回值是一个数组
              4. `getElementByName()`：根据Name属性值获取元素对象们。返回值是一个数组

              ```html
              <div class="cities">
                  <h2 class="ccc">London</h2>
                  <p id="2">
                      London is the capital city of England.
                      It is the most populous city in the United Kingdom,
                      with a metropolitan area of over 13 million inhabitants.
                  </p>
              </div>
              <input id="1" name="username" type="text" value="123">
              <script>
                  document.getElementById(2).innerHTML="奶茶妹妹";
                  document.getElementsByTagName("div");
                  document.getElementsByClassName("ccc");
                  document.getElementsByName("username");
              </script>
              ```

            * 创建其他DOM对象：

              1. `createAttribute(name)`：创建拥有指定名称的属性节点，并返回新的 Attr 对象。
              2. `createComment()`：创建注释节点。
              3. `createElement()`：创建元素节点。
              4. `createTextNode()`：创建文本节点。

              ```html
              document.createElement("div")
              ```

       * Element：元素对象

         * 创建（获取）通过document来获取创建
         * 方法
           1. `removeAttribute()`：删除指定的属性。
           2. `setAttribute()`：添加新属性。

       * Attribute：属性对象

       * Text：文本对象

       * Comment：注释对象

       * Node：节点对象，其他5个父对象

         * 特点：所有 dom 对都可以被认为是一个节点
         * 方法：crud dom树
           * appendChild()	向节点的子节点列表的结尾添加新的子节点。
           * removeChild()	删除（并返回）当前节点的指定子节点。
           * replaceChild()	用新节点替换一个子节点。
         * 属性
           * parentNode	返回节点的父节点。

       * 事例

       * `"delTr(this);"`：当前节点delTr方法名

         ```html
         <!DOCTYPE html>
         <html lang="en">
         <head>
             <meta charset="UTF-8">
             <title>function</title>
             <style>
                 table{
                     border: 1px solid;
                     margin: auto;
                     width: 500px;
                 }
                 td,th{
                     text-align: center;
                     border: 1px solid;
                 }
                 div{
                     text-align: center;
                     margin: 50px;
                 }
             </style>
         </head>
         <body>
         <div>
         <input id="input1" placeholder="请输入编号"/>
         <input id="input2" placeholder="请输入姓名"/>
         <input id="input3" placeholder="请输入性别"/>
         <input id="button" type="button" value="添加"/>
         </div>
         <table id="table1">
             <caption>学生信息表</caption>
             <tr id="tr1">
                 <td id="td1">编号</td>
                 <td id="td2">姓名</td>
                 <td id="td3">性别</td>
                 <td id="td4">操作</td>
             </tr>
         </table>
         <script>
             document.getElementById("button").onclick = function (){
                 var input1 = document.getElementById("input1").value;
                 var input2 = document.getElementById("input2").value;
                 var input3 = document.getElementById("input3").value;
         
                 var td_input1 = document.createElement("td");
                 var text_input1 = document.createTextNode(input1);
                 td_input1.appendChild(text_input1);
                 var td_input2 = document.createElement("td");
                 var text_input2 = document.createTextNode(input2);
                 td_input2.appendChild(text_input2);
                 var td_input3 = document.createElement("td");
                 var text_input3 = document.createTextNode(input3);
                 td_input3.appendChild(text_input3);
         
                 var td_a = document.createElement("td");
                 var property_a = document.createElement("a");
                 property_a.setAttribute("href","javascript:void(0);");
                 property_a.setAttribute("onclick","elTr(this);");
                 var text_a = document.createTextNode("删除");
                 property_a.appendChild(text_a);
                 td_a.appendChild(property_a);
         
                 var tr = document.createElement("tr");
                 tr.appendChild(td_input1);
                 tr.appendChild(td_input2);
                 tr.appendChild(td_input3);
                 tr.appendChild(td_a);
         
                 var table2 = document.getElementsByTagName("table")[0];
                 table2.appendChild(tr);
             }
             function elTr(obj){
                 var tebal = obj.parentNode.parentNode.parentNode;
                 var tr = obj.parentNode.parentNode;
                 tebal.removeChild(tr);
             }
         </script>
         </body>
         </html>

  2. XML DOM：针对 XML 文档的标准模型

  3. HTML DOM：针对 HTML 文档的标准模型

     * 设置获取标签体innerHTML；可以添加文本、标签，追加

     * innerHTML实现上面事例

       ```html
       <!DOCTYPE html>
       <html lang="en">
       <head>
           <meta charset="UTF-8">
           <title>function</title>
           <style>
               table{
                   border: 1px solid;
                   margin: auto;
                   width: 500px;
               }
               td,th{
                   text-align: center;
                   border: 1px solid;
               }
               div{
                   text-align: center;
                   margin: 50px;
               }
           </style>
       </head>
       <body>
       <div>
           <input id="input1" placeholder="请输入编号"/>
           <input id="input2" placeholder="请输入姓名"/>
           <input id="input3" placeholder="请输入性别"/>
           <input id="button" type="button" value="添加"/>
       </div>
       <table id="table1">
           <caption>学生信息表</caption>
           <tr id="tr1">
               <td id="td1">编号</td>
               <td id="td2">姓名</td>
               <td id="td3">性别</td>
               <td id="td4">操作</td>
           </tr>
       </table>
       <script>
           document.getElementById("button").onclick = function (){
               var input1 = document.getElementById("input1").value;
               var input2 = document.getElementById("input2").value;
               var input3 = document.getElementById("input3").value;
       
               var table = document.getElementsByTagName("table")[0];
       
               table.innerHTML += "<tr>\n"+
                   "<td>"+input1+"</td>\n"+
                   "<td>"+input2+"</td>\n"+
                   "<td>"+input3+"</td>\n"+
                   "<td><a href=\"javascript:void(0)\" onClick=\"elTr(this)\">删除</a></td>\n"+
               "</tr>";
           }
           function elTr(obj){
               var tebal = obj.parentNode.parentNode.parentNode;
               var tr = obj.parentNode.parentNode;
               tebal.removeChild(tr);
           }
       </script>
       </body>
       </html>
       ```

     * 控制样式

       1. 方式1：`document.gitElementById().style.css样式名="值"`，使用元素的style属性来设置
       2. 方式2：`document.gitElementById().className = "类选择器"`提前定义的class选择器样式，通过元素的className属性来设置class属性值。

## 事件

* 某些组件被执行了，某些操作后，触发某些代码执行
  * 绑定事件
    1. 直接在html标签上，指定事件属性（）
    2. `document.getElementById().事件`
  * 单击事件：`onclick`
  
* 事件

  1. 点击事件
     1. onclick	当用户点击某个对象时调用的事件句柄。
     2. ondblclick	当用户双击某个对象时调用的事件句柄。
  2. 焦点事件
     1. onblur	元素失去焦点时触发
     2. onfocus	元素获取焦点时触发
  3. 加载事件
     1. onload	一张页面或一幅图像完成加载。
  4. 鼠标事件
     1. onmousedown	鼠标按钮被按下。
        1. 定义一个形参，可以获取那个键
     2. onmouseup	鼠标按键被松开。
     3. onmousemove	鼠标被移动。
     4. onmouseover	鼠标移到某元素之上。
     5. onmouseout	鼠标从某元素移开。
  5. 键盘事件
     1. onkeydown	某个键盘按键被按下。		
     2. onkeyup	某个键盘按键被松开。
     3. onkeypress	某个键盘按键被按下并松开。
  6. 选中和改变
     1. onchange	该事件在表单元素的内容改变时触发`( <input>, <keygen>, <select>, 和 <textarea>)`
     2. onselect	用户选取文本时触发` ( <input> 和 <textarea>)`
  7. 表单事件
     1. onsubmit	表单提交时触发
     2. onreset	表单重置时触发

* 事例

  ```javascript
  //失去焦点
  document.getElementById("username").onblur = function(){}
  //加载事件
  window.onload=function(){}
  ```

## JQuery

1. Jquery对象和JS对象的区别与转换
   * jquery转换为js：`jquery对象[索引] 或者 jquery对象.get(索引)`
   * js转换为jquery：`$(js对象)`

2. 选择器：==选择据相似特征的元素（标签）==
   1. 基本语法
      * 事件绑定
         * `$("#id名称").事件名称(function(){});`
      * 入口函数
         * `$(function(){})`
      * 样式控制
         1. `$("#div1").css("样式名称"，"样式")`、`$("#div1").css("background-color"，"red")`
         2. DOM写法`$("#div1").css("backgroundColor"，"样式")`
   2. 选择器分类
      1. 基本选择器
         1. 标签选择器
            * 语法：`$("html 标签名")`获得所有匹配标签名称的元素
         2. id选择器
            * 语法：`$("#id的属性值")`获得与指定 id 属性值匹配的元素
         3. 类选择器
            * 语法：`$(".class的属性值")` 获得与指定的 class 属性值匹配的元素
         4. 并集选择器
            * `$("选择器1，选择器2，....")`获取多个选择器选中的所有元素
      2. 层级选择器
         1. 后代选择器
            * 语法：`$("A B "）`选择 A 元内部的所有 B 元素，包括B下的
         2. 子选择器
            * 语法：`$("A > B "）`选择 A 元内部的所有 B 子元素，不包括B下的
      3. 属性选择器
         1. 属性名称选择器
            * 语法：`$(A[属性名]")`包含指定属性的选择器
         2. 属性选择器
            * 语法：`$(A[属性名=值]")`包含指定属性等于指定值的选择器
         3. 复合属性选择器
            * 语法：`$(A[属性名=值][]....")`包含多个属性条件的选择器
      4. 过滤选择器
         1. 首元素过滤选择器
            * 语法：`:first` 获得选择的元素中的第一个元素`$(div:first).css`
         2. 尾元素过滤选择器
            * 语法：`:last` 获得选择的元素中的最后一个元素
         3. 非元素选择器
            * 语法：`:not(selecter)` 不包括指定内容的元
         4. 偶元素选择器
            * 语法：`:even` 偶数，从 0 开始计数
         5. 奇元素选择器
            * 语法：`:odd` 奇数，从 0 开始计数
         6. 等于索引选择器
            * 语法：`:eq(index)` 指定索引元素
         7. 大于索引选择器
            * 语法：`:gt(index)` 大于指定索引元素
         8. 小于索引选择器
            * 语法：`:lt(index)` 小于指定索引元素
         9. 标题选择器
            * 语法：`:header` 获得标题元素，固定写法==`<h1>到<h6>`==
      5. 表单过滤选择器
         1. 可用元素选择器
            * 语法：`:enabled` 获得可用元素
         2. 不可用元素选择器
            * 语法：`:disabled` 获得不可用元素
         3. 单选中选择器
            * 语法：`:checked` 获得单选/复选框选中的元素
         4. 复选中选择器
            * 语法：`:selected` 获得下拉框选中的元素

3. DOM操作

   1. 内容操作

      1. `html()` ：获取/设置元素的标签体内容 `<a><font> 内容 </font></a>    <font> 内容</font>`
      2. `text()` ：获取/设置元翠的标签体纯文本内容 `<a><font> 内容</font></a>    内容`
      3. `val()`：获取/设置元素的 value 属性值

   2. 属性操作

      1. 通用属性操作

         1. `attr()` ：获取/设置元素的属性

         2. `removeAttr()` ：删除属性

         3. `prop()` ：获取/设置元的属性

         4. `removeProp()` ：删除属性

            attr 和 prop 区别？

            1. 如果操作的是元素的固有属性，则建议使用 prop
            2. 如果操作的是元素自定义的属性，则建议使用 attr

      2. 对CLASS属性操作

         1. `addC1ass()`：添加 class 属性
         2. `removeclass()` ：删除 class 属性值
         3. `toggleclass()`：切换属性、如果存在就删除、如果不存在就添加

   3. CRUD操作

      1. `append()` ：父元将子元追加到末尾
         *  `对象1.append(对象2)`：将对象2 添加到对象1元素内部，并且在末尾
      2. `prepend()`：父元素将子元素追到开头
         * `对象1.prepend(对象2)` ：将对 2 添加到对 1 元内部，并且在开头
      3. `appendTo()`：
         * `对象1.appendTo(对象2)` ：将对象1 添加到对 2 内部，并且在末尾
      4. `prependTo()` ：
         * `对象1.prependTo(对象2)` ：将对对象1 添加到对象 2 内部，并且在开头
      5. `after()` ：添加元到元后边
         * `对象1.after(对象2)`：将对象 2 添加到对象 1 后边。对象 1 和对 2 是兄弟关系
      6. `before()` ：添加元到元前边
         * `对象1.before)对象2 )`：将对 2 添加到对 1 前边。对象1 和对象2 是兄弟关系
      7. `insertAfter()`
         * `对象1.insertAfter(对象2)` ：将对象2 添加到对象 1 后边。对象1 和对象2 是兄弟关系
      8. `insertBefore()`
         * `对象1.insertBefore(对象2)` ：将对象2 添加到对象1 前边。对象 1 和对象2 是兄弟关系
      9. `remove()` ：移除元素
         * `对象.remove()`：将对象删除掉
      10. `empty()` ：清空元素的所有后代元素。
          * `对象.empty()` ：将对象的后代元素全部清空，但是保当前对以及其属性节

4. 动画

   1. 三种方式显示隐藏元素

      1. 默认显示和隐藏方式

         1. `show([speed],[easing],[fn])`

            ```js
            $("#id").show("slow","linear",function(){})
            ```

         1. `hide([speed],[easing],[fn])`
         2. `toggle([speed],[easing],[fn])`

      2. 滑动显示和隐藏方式

         1. `slideDon([speed],[easing],[fn])`
         2. `slideUp([speed],[easing],[fn])`
         3. `slideToggle([speed],[easing],[fn])`

      3. 淡入淡出显示和隐藏方式

         1. `fadeIn([speed],[easing],[fn])`
         2. `fadeOut([speed],[easing],[fn])`
         3. `fadeToggle([speed],[easing],[fn])`

   2. 参数

      1. `speed` ：动画的速度。三个定义的值`("slow","normal","fast")`或表示动画时长的毫秒数值（如：10000）
      2. `easing` ：用来指定切换效果，默认是 "swing",可用参数"linear"
         * swing ：动画执行时效果是先慢，中间快，最后又慢
         * linear ：动画执行时速度是匀速的
      3. `fn` ：在动画完成时执行的函数，每个元素执行一次。： IOOØ ）

5. 遍历

   1. js遍历方式

      * for(初始化值，循环结束条件，步长)

   2. jq遍历方式

      * `jquery对象.each(callback)`

         ```js
         <ul id="city">
             <li></li>
         </ul>
         
         <script>
             city.each(function(index,element){
             //1. 获取li对象this
             alert(this.innerHTML)//innerHTML获取标签内的值
             $(this).html();//html()获取标签内的值
             //2. 在会掉函数中定义参数，第一个是索引，第二个是元素对象
             return false;//结束循环
             return false;//结束本次循环,继续下次循环
             element.innerHTML;
             $(element).html();
         })
         </script>
         ```

      * `$.each(Object,[callback])`

         ```js
         $.each(city,function(){
             $(this).html();
         });
         ```

      * `for…fo:`

         ```js
         for(li of city){
             $(li).html();
         }
         ```

6. 事件绑定

   1. jquery标准绑定方式

      * `jquery对象.事件方法(回调函数)`

   2. on绑定事件/off解除绑定

      * `jquery对象.on(“事件名称”,回调函数)`

      * `jquery对象.off(“事件名称”)`

         ```js
         $("").on("click",function(){});
         $("").off("click");//不传递参数解除所有绑定
         ```

   3. 事件切换：toggle

      * `jquery对象.toggle(fn1,fn2...)`：方法1，方法2

7. 插件：增强jquery的功能

   1. 实现方式

      1. `$.fn.extend(object)`

         * 增强通过 Jquery 获取的对象的功能 $("#id")

      2. `$.extend(object)`

         * 增强jquery对象自身的功能 `$/jquery`

         ```js
         $.fn.extend({
             方法名称:function(){
                 //定又了一个方法。所有的 jq 对象都可以调用该方法
             }
         });
         ```

## js数据展示

### AJAX

1. 概念

   1. AJAX 是一种在无需重新加载整个网页的倩况下，能够更新部分网页的技术。
   2. 异步和同步，客户端和服务器端相互通信的基础上
      * 客户端必须等待服务器端的响应。在等待的期间客户端不能做其他操作。
      * 客户端不需要等待服务器端的响应。在服务器处理请求的过程中，客户端可以进行其他的操作。

2. 实现

   1. 原生js方式

      1. 实现步骤

         ```js
         //定义方法
         function fun(){
         //发送异步请求
         //1. 创建核心对象
             const xhttp = new XMLHttpRequest();  
         //2. 定义回调函数
             xhttp.onload = function() {
           // 您可以在这里使用数据
             }
         //3. 发送请求
             xhttp.open("GET", "ajax_info.txt");
             xhttp.send();
         //4.处理响应
             xhttp.onreadystatechange = function() {
                 if (this.readyState == 4 && this.status == 200) {
                     xhttp.responseText;//获取服务器传来的值
                }
             };
         }
         ```

      2. 如需向服务器发送请求，您可以使用 XMLHttpRequest 对象的 `open()` 和 `send()` 方法

         1. `open("请求方式","请求的URL",同步或异步)`
         2. true异步、false同步
         3. get请求传入的参数xie在open()方法的请求URL后面。post请求写在send()方法里面

   2. jq方式

      1. `$.ajsx()`

         1. 实现步骤

            ```js
            //定义方法
            function fun(){
                $.ajax({
                    url:"",//请求路径
                    type:"",//请求方式
                    data:{json},//请求参数
                    success:function(){},//响应成功后的回调函数
                    error:function(){},//响应错误后的回调函数
                    dataType:""//设置接收到的响应数据格式
                });
            }
            ```

      2. `$.get()`：对于不同请求的单独封装

         1. 实现步骤：发送get请求

         2. 语法：`$.get(url,[data].[callback],[type])`

            参数：

            * url：请求路径
            * data：请求参数
            * callback：回调函数
            * type：响应结果的类型

            ```js
            $.get("",{josn},function(){},json)

      3. `$.post()`：发送post请求、与get方法只是方法名不同

### JSON

==js对象表示法、JSON 是一种存储和交换数据的语法。==

1. 基本规则

   1. 数据在名称/键值对中： JSON 数据是由值对构成的
      * 键用引号（单双都行）引起来，也可以不使用引号
      * 值得取值类型：
         1. 字符串：在双引号中
         2. 数字：整数或浮点数
         3. 对象（JSON 对象）：在花括号中
         4. 数组：在方括号中：`{"":[{},{}]}`
         5. 布尔：true或者false
         6. null
   2. 数据由逗号分隔：多个键值队由逗号分隔
   3. 花括号容纳对象：使用{}定义JSON
   4. 方括号容纳数组：[]

2. 获取数据

   1. 获取方式

      1. json对象.键名
      2. `json对象[“键名”]`
      3. 数组对象[索引]

   2. 遍历

      ```json
      var pse = {"123":"123","123"123:,"123",true}
      for(var key in pse){
          key+pse[key];
      }
      var ps = {["123":"123","123"123:,"123",true],
                 ["123":"123","123"123:,"123",true],
                 ["123":"123","123"123:,"123",true]}
      for(var i = 0;i<ps.length;i++){
          var p = ps[i];
          for(var key in p){
          key+p[key];
      }
      }
      ```

   3. json数据和java对象的相互转换

      * 解析器
         1. 常见解析器：jsonlib、gson、fastjson、`jackson：springMVC自带的解析器`

      1. json转Java

         1. 导入 jackson 的相关 jar 包
         2. 创建 Jackson 核心对象 objectmapper
         3. 调用 objectmapper 的相关方法进行转换
            1. 方法：`readValue(json字符串，javabean.class)`

      2. java转json

         1. 使用步骤

         2. 导入 jackson 的相关 jar 包

            ```
            jackson-core
            jackson-databind
            jackson-annotations
            ```

         3. 创建 Jackson 核心对象 objectmapper

         4. 调用 objectmapper 的相关方法进行转换

            ```java
            public void tun() {
                //创建Java对象    
                JsonPrsom json = new JsonPrsom();        
                json.setId(1);    
                json.setUsername("张三");    
                json.setPassword("219798");    
                //
                ObjectMapper mapper = new ObjectMapper();    
                try {    
                    String s = mapper.writeValueAsString(json);        
                    System.out.println(s);        
                } catch (JsonProcessingException e) {    
                    throw new RuntimeException(e);        
                }    
            }
            ```

         5. 转换方法

            1. writeVa1ue(参数1，obj)：
            2. 参数1
               * File：将 obj 对象转换为 json 字符串，并保存到指定的文件中
               * `mapper.writeValue(new File(),对象);`
               * Writer：将 obj 对象转换为 json 字符串，并将 json 数据填充到字符输出流中
               * 0utputStream ：将 obj 对象转换为 json 字符串，并将 json 数据填充到字节输出流中
            3. writeVa1ueAsString(obj) ：将对象转为json字符串

         6. 注解：写在bean里面

            1. `@JsonIgnore`：排除属性
            2. `@JsonFormat`：属性值格式化

         7. 复杂java对象转换：转换方式一样

            1. List：数组
            2. Map：对象格式一致

