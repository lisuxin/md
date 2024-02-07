#### 在 Python 中使用 Pi

使用 `math.pi()` 函数在 Python 中获取 Pi 值

使用 `numpy.pi()` 函数在 Python 中获取 Pi 值

使用 `scipy.pi()` 函数在 Python 中获取 Pi 值

使用 `math.radians()` 函数在 Python 中获取 Pi 值

Python 有很多对象和模块可用于数学和科学计算。

在本教程中，我们将在 Python 中查找并使用 pi 值。

#### 使用 `math.pi()` 函数在 Python 中获取 Pi 值

为此，我们将使用 `math` 模块。`math` 模块提供对 Python 编程语言中数学函数的访问。

这个模块有很多相关的功能。`pi` 函数用于在 Python 中访问 pi 的值。首先，导入 `math` 模块以访问 `pi` 函数。

例如，

```python
import math
math.pi
```

输出：

```text
3.141592653589793
```

我们现在可以将此值用于我们的计算和表达式。

#### 使用 `numpy.pi()` 函数在 Python 中获取 Pi 值

`numpy.pi()` 也可以在 Python 中返回 pi 的值。

例如，

```python
import numpy
print(numpy.pi)
```

输出：

```text
3.141592653589793
```

#### 使用 `scipy.pi()` 函数在 Python 中获取 Pi 值

来自 `scipy` 模块的 `pi()` 函数也可以返回 pi 的值。

```python
import scipy
print(scipy.pi)
```

输出：

```text
3.141592653589793
```

所有三个模块都返回相同的值。这个函数存在于三个模块中的唯一原因是它允许我们在不导入任何其他模块的情况下使用 pi 值。例如，在使用 `NumPy` 时，我们不必导入 `math` 或 `scipy` 来获取 pi 的值。

#### **使用 `math.radians()` 函数在 Python 中获取 Pi 值**

这是一种非常规的方法，几乎从未使用过。还有另一种方法可以在 Python 中将度数转换为弧度，而无需针对特定情况直接处理 pi。在 `math` 模块中有一个名为 `radians()` 的函数将度数转换为弧度。

```python
import math
math.radians(90)
```

输出：

```text
1.5707963267948966
```

我们可以使用这个函数来获取 pi 的值，如下图。

```python
import math
math.radians(180)
```

输出：

```text
3.141592653589793
```

如你所见，当我们将 180 度转换为弧度时，我们得到了 pi 的值