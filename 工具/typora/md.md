# 标题

[toc]

```
标题名字（#号的个数代表标题的级数，有几个#号就代表几级标题）
```

# 一级标题使用1个#

## 二级标题使用2个#

### 三级标题使用3个#

#### 四级标题使用4个#

##### 五级标题使用5个#

###### 六级标题使用6个#

```
#最多支持六级标题#
```



#### 目录`[toc]`

## 文字

### 删除线

```
这就是 ~~删除线~~（使用波浪号）
```

这就是 ~~删除线~~（使用波浪号）

### 斜体

```
这是用来 *斜体* _文本_
快捷键ctrl+i
```

这是用来 *斜体* _文本_

### 加粗

```
这是用来 **加粗** _文本_
快捷键 ctrl+b
```

这是用来 **加粗** 文本

### 斜体+加粗

```
这是用来 ***斜体+加粗*** _文本_
```

这是用来 ***斜体+加粗*** _文本_

### 下划线

```
1.下划线是HTML的语法
2.下划线快捷键（ctrl+u）
3.<u>下划线</U>
```

<u>下划线</u>

### 高亮（需要勾选扩展语法）

```
这是用来 ==高亮的== 文本
```

这是用来 ==高亮的==  文本

### 下标(需要勾选扩展语法)

```
水 H~2~O
双氧水 H~2-O~2~
$\vec{a}$  向量
$\overline{a}$ 平均值
$\widehat{a}$ (线性回归，直线方程) y尖
$\widetilde{a}$ 颚化符号  等价无穷小
$\dot{a}$   一阶导数
$\ddot{a}$  二阶导数
```

水 H~2~O
双氧水 H~2~O~2~

$\vec{a}$  向量
$\overline{a}$ 平均值
$\widehat{a}$ (线性回归，直线方程) y尖
$\widetilde{a}$ 颚化符号  等价无穷小
$\dot{a}$   一阶导数
$\ddot{a}$  二阶导数

### 上标（需要勾选扩展语法）

```
面积：m^2^
体积：m^3^
```

面积：m^2^
体积：m^3^

### 搜索

```
ctrl+shift+f
```

### 表情符号

```
Emoji支持表情符号,你可以用系统默认的Emoji.也可以用图片的表情，输入`:`将会出现智能提示
```

#### 一些表情例子

```
:smile: :laughing: :dizzy_face: :sob: :cold_sweat: :sweat_smile: :cry: :triumph: :heart_eyes: :relaxed: :sunglasses: :weary:

:+1: :—1: :100: :clap: :bell: :gift: :question: :bomb: :heart: :coffee: :cyclone: :bow: :kiss: :pray: :sweat_drops: :hankey: :exclamation: :anger:
快捷键win+.
```

:smile: :laughing: :dizzy_face: :sob: :cold_sweat: :sweat_smile: :cry: :triumph: :heart_eyes: :relaxed: :sunglasses: :weary: :+1: :—1: :100: :clap: :bell: :gift: :question: :bomb: :heart: :coffee: :cyclone: :bow: :kiss: :pray: :sweat_drops: :hankey: :exclamation: :anger:

### 表格

使用`|`来分隔不同的单元格，使用`-`来分隔表头和其他行：

```\
快捷键ctrl + t
```

```
name | price
--- | ---
fried chicken | 19
cola | 5
```

为了使Markdown更清晰，`|`和`-`需要至少一个空格（最左侧和最右侧的`|`外就不需要了）

| name          | price |
| ------------- | :---: |
| fried chicken |  19   |
| cola          |   5   |

### 引用

```
>"后悔创业"
```

> "后悔创业"

```
>也可以在引用中
>>使用嵌套的应用
```

>也可以在引用中
>
>>使用嵌套的应用

### 列表

##### 无序列表--符号 空格

```
* 可以使用`*`作为标记
+ 也可以使用`+`
- 或者`-`
在符号后面加空格
```

* 可以使用`*`作为标记
+ 也可以使用`+`

- 或者`-`
- 结束列表在引用的前后都需要插入一个空白行, 如果在引用前没有插入空白行会导致引用之后的段落也被标记成引用, 中间再加入多个空白行都还是被引用状态, 只有在引用前后都插入空白行才可以解决.

### **

##### 有序列表--数字.空格

```
1. 有序列表以数字和`.`开始；
2. 数字的序列并不会影响生成的有序列表序列；
3. 但任然推荐按照自然顺序编写(1.2.3.4.5....)；
```

1. 有序列表以数字和`.`开始；

2. 数字的序列并不会影响生成的有序列表序列；

3. 但任然推荐按照自然顺序编写(1.2.3.4.5....)；

   ```
   可以使用：数字\.来取消显示为列表（用反斜杠进行转义）
   ```

   

## 代码

### 代码块

·```· 语言名称

输入HTML公式：`<!DOCTYPE html>`

### 行类代码

```
通过 `插入行类代码`
```

通过 `插入行类代码`

### 转换规则

代码块中的文本（包括Markdown语法）都会转换为原始类容

### 分割线

可以在一行中使用三个或者更多的`*`、`----`或`__`来添加分割线（``）:

```
***
----
____
```

***
----
____

### 跳转

#### 外部跳转--超链接

格式为`[link text](link)`。

```
[帮助文档](https://support.typora.io/Links/#faq)
按住ctrl+鼠标点击才会跳转
```

[帮助文档](https://support.typora.io/Links/#faq)

#### 内部跳转--文本件内跳（Typora支持）

格式为`[link text](link)`。

#### 1.黑板粗体：`\mathbb{ }`

黑板粗体（`[Blackboardbold`](https://links.jianshu.com/go?to=http%3A%2F%2Fen.wikipedia.org%2Fwiki%2FBlackboard_bold)）一般用于表示**数学和物理学中的向量或集合**的符号

大写：![\mathbb{ABCD}](https://math.jianshu.com/math?formula=%5Cmathbb%7BABCD%7D)
 小写：![\mathbb{abcd}](https://math.jianshu.com/math?formula=%5Cmathbb%7Babcd%7D)
 普通：`abcd`

```ruby
$\mathbb{ABCD}$
$\mathbb{abcd}$
```

#### 2.正粗体:`\mathbf{ }`

大写：![\mathbf{ABCD}](https://math.jianshu.com/math?formula=%5Cmathbf%7BABCD%7D)

普通：`ABCD`

Md加粗：`**ABCD**`

```ruby
$\mathbf{ABCD}$
ABCD
**ABCD**
$\mathbf{ \alpha}$
```

#### 3.斜体数字：`\mathit{}`

`\mathit斜体`：![\mathit{1234567890}](https://math.jianshu.com/math?formula=%5Cmathit%7B1234567890%7D)

Md斜体：*1234567890*



```ruby
$\mathit{1234567890}$
*1234567890*
```

在md下也可以用`* 斜体*`*斜体效果*

#### 4.罗马体:\mathrm{} or \mbox{ }

\mathrm罗马体:![\mathrm{ABCDEFG}](https://math.jianshu.com/math?formula=%5Cmathrm%7BABCDEFG%7D)
 \mbox{}   罗马体 :![\mbox{ABCDEFG}](https://math.jianshu.com/math?formula=%5Cmbox%7BABCDEFG%7D)

普通：`ABCDFEG`

```ruby
$\mathrm{ABCDEFG}$
ABCDFEG
$\mbox{ABCDEFG}$
```

#### 5.哥特体：`\mathfrak{}`

![\mathfrak{ABCDEFGHIJKLMNOPQRSTUVWXYZ}](https://math.jianshu.com/math?formula=%5Cmathfrak%7BABCDEFGHIJKLMNOPQRSTUVWXYZ%7D)

![\mathfrak{abcdefghijklmnopqrstuvwxyz}](https://math.jianshu.com/math?formula=%5Cmathfrak%7Babcdefghijklmnopqrstuvwxyz%7D)



```ruby
$\mathfrak{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$

$\mathfrak{abcdefghijklmnopqrstuvwxyz}$
```

#### 6.手写体：`\mathcal{}`

![\mathcal{ABCDEFGHIJKLMNOPQRSTUVWXYZ}](https://math.jianshu.com/math?formula=%5Cmathcal%7BABCDEFGHIJKLMNOPQRSTUVWXYZ%7D)

![\mathcal{abcdefg}](https://math.jianshu.com/math?formula=%5Cmathcal%7Babcdefg%7D)



```ruby
$\mathcal{ABCDEFGHIJKLMNOPQRSTUVWXYZ}$

$\mathcal{abcdefg}$
```



```
├── build
├── config
├── docs
│   └── static
│       ├── css
│       └── js
├── src
│   ├── assets
│   ├── components
│   ├── store
│   │   └── modules
│   └── views
│       ├── book
│       └── movie
└── static
└──
```



| 符号                  | 代码                    | 描述       |
| --------------------- | ----------------------- | ---------- |
| ∑                     | `$\sum$`                | 求和公式   |
| ∑*i*=0*n*             | `$\sum_{i=0}^n$`        | 求和上下标 |
| ×                     | `$\times$`              | 乘号       |
| ±                     | `$\pm$`                 | 正负号     |
| ÷                     | `$\div$`                | 除号       |
| ∣                     | `$\mid$`                | 竖线       |
| ⋅                     | `$\cdot$`               | 点         |
| ∘                     | `$\circ$`               | 圈         |
| $\ast $               | `$\ast $`               | 星号       |
| ⨂                     | `$\bigotimes$`          | 克罗内克积 |
| ⨁                     | `$\bigoplus$`           | 异或       |
| ≤                     | `$\leq$`                | 小于等于   |
| ≥                     | `$\geq$`                | 大于等于   |
| ̸=                     | `$\neq$`                | 不等于     |
| ≈                     | `$\approx$`             | 约等于     |
| $\prod$               | `$\prod$`               | N元乘积    |
| $\coprod$             | `$\coprod$`             | N元余积    |
| ⋯                     | `$\cdots$`              | 省略号     |
| ∫                     | `$\int$`                | 积分       |
| ∬                     | `$\iint$`               | 双重积分   |
| ∮                     | `$\oint$`               | 曲线积分   |
| ∞                     | `$\infty$`              | 无穷       |
| ∇                     | `$\nabla$`              | 梯度       |
| ∵                     | `$\because$`            | 因为       |
| ∴                     | `$\therefore$`          | 所以       |
| ∀                     | `$\forall$`             | 任意       |
| ∃                     | `$\exists$`             | 存在       |
| ̸>                     | `$\not>$`               | 不大于     |
| ≤                     | `$\leq$`                | 小于等于   |
| ≥                     | `$\geq$`                | 大于等于   |
| ̸⊂                     | `$\not\subset$`         | 不属于     |
| ∅                     | `$\emptyset$`           | 空集       |
| ∈                     | `$\in$`                 | 属于       |
| ∈/                    | `$\notin$`              | 不属于     |
| ⊂                     | `$\subset$`             | 子集       |
| ⊆                     | `$\subseteq$`           | 真子集     |
| ⋃                     | `$\bigcup$`             | 并集       |
| ⋂                     | `$\bigcap$`             | 交集       |
| ⋁                     | `$\bigvee$`             | 逻辑或     |
| ⋀                     | `$\bigwedge$`           | 逻辑与     |
| ⨄                     | `$\biguplus$`           | 多重集     |
| ⨆                     | `$\bigsqcup$`           |            |
| *y*^                  | `$\hat{y}$`             | 期望值     |
| *y*ˇ                  | `$\check{y}$`           |            |
| *y*˘                  | `$\breve{y}$`           |            |
| $\overline{a+b+c+d}$  | `$\overline{a+b+c+d}$`  | 平均值     |
| $\underline{a+b+c+d}$ | `$\underline{a+b+c+d}$` |            |
| ↑                     | `$\uparrow$`            | 向上       |
| ↓                     | `$\downarrow$`          | 向下       |
| $\Uparrow$            | `$\Uparrow$`            |            |
| ⇓                     | `$\Downarrow$`          |            |
| →                     | `$\rightarrow$`         | 向右       |
| ←                     | `$\leftarrow$`          | 向左       |
| ⇒                     | `$\Rightarrow$`         | 向右箭头   |
| ⟸                     | `$\Longleftarrow$`      | 向左长箭头 |
| ⟵                     | `$\longleftarrow$`      | 向左单箭头 |
| ⟶                     | `$\longrightarrow$`     | 向右长箭头 |
| ⟹                     | `$\Longrightarrow$`     | 向右箭头   |
| *α*                   | `$\alpha$`              |            |
| *β*                   | `$\beta$`               |            |
| *γ*                   | `$\gamma$`              |            |
| Γ                     | `$\Gamma$`              |            |
| *δ*                   | `$\delta$`              |            |
| Δ                     | `$\Delta$`              |            |
| *ϵ*                   | `$\epsilon$`            |            |
| *ε*                   | `$\varepsilon$`         |            |
| *ζ*                   | `$\zeta$`               |            |
| *η*                   | `$\eta$`                |            |
| *θ*                   | `$\theta$`              |            |
| Θ                     | `$\Theta$`              |            |
| *ϑ*                   | `$\vartheta$`           |            |
| *ι*                   | `$\iota$`               |            |
| *π*                   | `$\pi$`                 |            |
| *ϕ*                   | `$\phi$`                |            |
| *ϕ*                   | `$\phi$`                |            |
| *ψ*                   | `$\psi$`                |            |
| Ψ                     | `$\Psi$`                |            |
| *ω*                   | `$\omega$`              |            |
| Ω                     | `$\Omega$`              |            |
| *χ*                   | `\chi`                  |            |
| *ρ*                   | `$\rho$`                |            |
| *ο*                   | `$\omicron$`            |            |
| *σ*                   | `$\sigma$`              |            |
| Σ                     | `$\Sigma$`              |            |
| *ν*                   | `$\nu$`                 |            |
| *ξ*                   | `$\xi$`                 |            |
| *τ*                   | `$\tau$`                |            |
| *λ*                   | `$\lambda$`             |            |
| Λ                     | `$\Lambda$`             |            |
| *μ*                   | `\mu`                   |            |
| ∂                     | `$\partial$`            |            |
| {}                    | `$\lbrace \rbrace$`     |            |
| $\overline{a}$        | `$\overline{a}$`        |            |
| $\infty$              | `$\infty$`              |            |

## 关系运算符

| 输入        | 显示        | 输入         | 显示         | 输入        | 显示        | 输入       | 显示         |
| ----------- | ----------- | ------------ | ------------ | ----------- | ----------- | ---------- | ------------ |
| \pm         | $\pm$       | \times       | $\times$     | \div        | $\div$      | \mid       | $\mid$       |
| \nmid       | $\nmid$     | \cdot        | $\cdot$      | \circ       | $\circ$     | `\ast`     | $\ast$       |
| `\bigodot`  | $\bigodot$  | `\bigotimes` | $\bigotimes$ | `\bigoplus` | $\bigoplus$ | \leq       | $\leq$       |
| \geq        | $\geq$      | \neq         | $\neq$       | \approx     | $\approx$   | \equiv     | $\equiv$     |
| \sum        | $\sum$      | \prod        | $\prod$      | \coprod     | $\coprod$   | \backslash | $\backslash$ |
| `\geqslant` | $\geqslant$ | `\leqslant`  | $\leqslant$  |             |             |            |              |
