# Numpy

### N维数组对象：ndarray

数组对象可以去掉元素间运算所需的循环，使一维向量更像一个单个数据；

通过设置专门的数组对象，经过优化，可以提升这类应用的运算速度。

注：Numpy的底层实现是由C语言实现的。

观察：科学计算中，一个维度中所有数据的类型往往相同

数组对象采用相同的数据类型，有助于节省运算和存储空间。

ndarray是一个多维数组对象，由两部分构成：

1实际的数据

2描述这些数据的元数据（数据维度，数据类型等）

ndarray数组一般要求所有元素类型相同（同质），数组下标从0开始。



np.array()生成一个ndarray数组

ndarray在程序中的别名是：array

np.array()输出[]形式，元素由空格分割。

轴（axis）：保存数据的维度 

秩（rank）：轴的数量

ndarray对象的属性

| .ndim     | 秩                              |
| --------- | ------------------------------- |
| .shape    | 尺度，n行m列                    |
| .size     | 元素个数，相当于.shape中n*m的值 |
| .dtype    | 元素类型                        |
| .itemsize | 元素的大小，以字节为单位        |

###### ndarray的元素类型

| 数据类型   | 说明                               |
| :--------- | ---------------------------------- |
| bool       |                                    |
| inte       |                                    |
| intp       |                                    |
| int8       |                                    |
| int16      |                                    |
| int32      |                                    |
| int64      |                                    |
| uint8      | 8位无符号整数，取值：【0，255】    |
| uint16     |                                    |
| unit32     |                                    |
| unit64     |                                    |
| float16    |                                    |
| float32    | 16位版精度浮点数：1位符号数        |
| float64    |                                    |
| complex32  | 复数类型：实部和虚部都是32位浮点数 |
| compllex64 |                                    |

Python语法仅支持整数、浮点数和复数3种类型

科学计算涉及数据较多，对存储和性能都有较高要求。

对于元素类型精细定义，有助于NumPy合理使用存储空间并优化性能。

对元素类型精细定义，有助于程序员对程序规模有合理评估。

ndarray数组可以由非同质对象构成

非同质ndarray元素为对象类型

非同质ndarray对象无法有效发挥numopy优势，尽量避免使用

## ndarray数组的创建和变化

ndarray数组的创建方法

（1）从Pythopn中的列表、元组等类型船舰ndarray数组。

```Python
x= np.array(list/tuple,dtype=float32)
```

当np.array（）不指定dtype时，NumPy将根据数据关联情况关联一个dtype类型。

<1>从列表类型

<2>从数组类型

<3>从列表类型混合创建

（2）使用numpy中函数创建ndarray数组，如arange，noes，zeros等。

| 函数                              | 说明                                                         |
| :-------------------------------- | ------------------------------------------------------------ |
| np.arange(n)                      | 类似range函数，返回ndarray类型，元素从0到n-1                 |
| np.ones(shape)                    | 根据shape生成一个全1数组，shape是元组类型                    |
| np.zeros(shape)                   | 根据shape生成一个全0数组，shape是元组类型                    |
| np.full(shape,val)                | 根据shape生成一个数组，每个元素值都是val                     |
| np.eye(n)                         | 创建一个正方的n*n单位矩阵，对角线为1，其余为0                |
| np.ones_like(a)                   | 根据数组a的形状生成一个全1数组                               |
| np.zeros_like(a)                  | 根据数组a的形状生成一个全0数组                               |
| np.full_like(a,val)               | 根据数组a的形状生成一个数组，每个元素值都是val               |
| np.linspace(a,b,c,endpoint=False) | 根据起止数据等间距地填充数据，形成数组 a为起始数值，b为终止数值，c为生成间隔,endpoint指b是否作为生成数组的终值。 |
| np.concatenate()                  | 将两个或多个数组合并成一个新的数组                           |

（3）从字节流（raw bytes ）中创建ndarray数组。

（4）从文件中读取特定格式，创建ndarray数组。

## ndarray数组的变换

对于创建后的ndarray数组，可以对其进行维度变换和元素类型变换。

| 方法               | 说明                                                |
| ------------------ | --------------------------------------------------- |
| .reshape(shape)    | 不改变数组元素，返回一个shape形状的数组，原数组不变 |
| .resize(shape)     | 与reshape()功能一致，但修改原数组                   |
| .swapaxes(ax1,ax2) | 将数组n个维度中两个维度进行调换                     |
| .flatte()          | 对数组进行降维，返回折叠后的一维数组，原数组不变    |

```python
a = np.ones((2,3,4), dtype = np.int32)
new_a = a.astype(new_type)
```

astype()方法一定会创建新的数组（原始数据的一个copy），即使两个类型一致。

`ls = a.tolist()`

## ndarray数组的索引和切片

###### 索引：获取数组中特定位置元素的过程

##### 切片：获取数组元素子集的过程

一维数组的索引和切片：与python的列表相似

`a[2]`

`a[a:b:c]` a:起始编号；b:终止编号（不含）；c:步长

多维数组的索引和切片：

`a= np.arange(24).reshape((2,3,4))`

a array([

]

)

a[1,2,3] 每个维度索引值之间用逗号分隔，每个维度切片方法和一维数组相同，每个维度可以使用步长跳跃切片

## ndattay数组的运算

###### 1.数组与标量之间的运算

数组与标量之间的运算作用于数组的每一个元素

eg：`a = a/a.mean()`

###### 2.Numpy一维运算函数元素级运算的函数

| 函数                                                         | 说明                                               |
| :----------------------------------------------------------- | -------------------------------------------------- |
| `np.abs(x) `/`np.fabs()`                                     | 计算函数个元素的绝对值                             |
| `np.sqrt()`                                                  | 计算函数各元素的平方根                             |
| `np.square(x)`                                               | 计算数组各元素的平方                               |
| `np.log(x)`/`np.log10(x)`/`np.log2(x)`                       | 计算数组各元素的自然对数、10底对数、2底对数        |
| `np.ceil(x)`/`np.floor(x)`                                   | 计算数组各元素的ceiling值和floor值                 |
| `np.rint(x)`                                                 | 计算数组各元素的四舍五入值                         |
| `np.modf(x)`                                                 | 将数组个元素的小数和整数部分以两个独立数组形式返回 |
| `np.cos(x)`  `np.cosh(x)` <br />`np.sin(x)`  `np.sinh(x)`<br />`np.tan(x)`  `np.tanh(x)` | 计算数组各元素的普通型和双曲型三角函数             |
| `np.exp(x)`                                                  | 计算数组各元素的指数值                             |
| `np.sign(x)`                                                 | 计算数组各元素的符号值，1（+），0，-1（-）         |

###### 3.Numpy二元函数

| 函数                                                         | 说明                                       |
| ------------------------------------------------------------ | :----------------------------------------- |
| `+` `-` `*` `/` `**`                                         | 两个数组个元素进行对应运算                 |
| `np.maximum(x,y)` `np.fmax()`<br />`np.minimum(x,y)`  `np.min()` | 元素级的最大值/最小值计算                  |
| `np.mod(x,y)`                                                | 元素级的模运算                             |
| `np.copysign(x,y)`                                           | 将数组y中各元素值的符号赋值给数组x对应元素 |
| `><` `>=` `<=` `==` `!=`                                     | 算数比较，产生布尔型数组                   |

## CSV文件

`np.savetxt(frame,array,fmt='%.18e',dilimiter=None)`

frame：文件、字符串或产生器，可以是.gz或.bz2的压缩文件

array：存入文件的数组

fmt：写入文件的格式，例如：%d %.2f) %.18e

delimiter ：分割字符串，默认是任何空格

eg：

```python
a = np.arange(100).reshape(5,20)
np.savetxt('a.csv',a,fmt='%d',delimiter=',')
```

`np.loadtxt(frame,dtype=np.float,delimiter=None,unpack=False)`

frame：文件、字符串或产生器，可以是.gz或.bz2的压缩文件。

dtype：数据类型，可选。

delimiter ：分割字符串，默认是任何空格

unpack: 如果TRUE，读入属性将分别写入不同变量

csv文件的局限性

csv只能有效存储一维和二维数组

## Numpy库的随机数函数

| 函数                        |                             说明                             |
| --------------------------- | :----------------------------------------------------------: |
| `rand(d0,d1...dn)`          |       根据d0-dn创建随机数数组，浮点数，[0,1)，均匀分布       |
| `randn(d0,d1...dn)`         |            根据d0-dn创建随机数数组，标准正态分布             |
| `randint(low,high,(shape))` |      根据shape创建随机整数或整数数组，范围是[low,high)       |
| `seed(s)`                   |                 随机数种子，s是给定的种子值                  |
| `shuffle(a)`                |           根据数组a的第1轴进行随机排列，改变数组x            |
| `permutation(a)`            |      根据数组a的第1轴产生一个新的乱序数组，不改变数组x       |
| `choice(a,size,replace,p)`  | 从一维数组a中以概率p抽取元素，形成size形状的新数组replace表示是否可以重用元素，默认为False |
| `uniform(low,high,size)`    |    产生具有均匀分布的数组，low起始值high结束值，size形状     |
| `normal(loc,scale,size)`    |    产生具有正态分布的数组，loc均值，scale标准差，size形状    |
| `poissnon(lam,size)`        |     产生具有泊松分布的数组，lam随机事件发生率，size形状      |

```python
np.random.choice(b,(3,2),p=b/np.sum(b))
```

## Numpy的统计函数

| 函数                                | 说明                                                  |
| ----------------------------------- | ----------------------------------------------------- |
| `sum(a,axis=None)`                  | 根据给定轴axis计算数组a相关元素之和，axis整数或元组   |
| `mean(a,axis=None)`                 | 根据给定轴axis计算数组a相关元素的期望，axis整数或元组 |
| `average(a,axis=None,weights=None)` | 根据给定轴axis计算数组a相关元素的加权平均值           |
| `std(a,axis=None)`                  | 根据给定轴axis计算数组a相关元素的标准差               |
| `var(a,axis=None)`                  | 根据给定轴axis计算数组a相关元素的方差                 |
| `min(a)` `max(a)`                   | 计算数组a中元素的最小值、最大值                       |
| `argmin(a)`  `argmax(a)`            | 计算数组a中元素最小值、最大值的降一维后下标           |
| `unravel_index(index,shape)`        | 根据shape将一维下标index转换为多维下标                |
| `ptp(a)`                            | 计算数组a中最大值最小值的差                           |
| `median(a)`                         | 计算数组a中元素的中位数（中值）                       |

