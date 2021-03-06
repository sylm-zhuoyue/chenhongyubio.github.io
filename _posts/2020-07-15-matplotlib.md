---
layout: post # 使用的布局（不需要改）
title: matplotlib # 标题
subtitle: Python中matplotlib库的学习 #副标题
date: 2020-07-15 # 时间
author: CHY # 作者
header-img: img/wallhaven-matplotlib.jpg #这篇文章标题背景图片
catalog: true # 是否归档
tags: #标签
  - 计算机
---

#### matplotlib 简介

![matplotlib绘图元素](https://github.com/chenhongyubio/chenhongyubio.github.io/raw/master/img/matplotlib绘图元素.png)<br>

1. figure<br>
   figure 是图片的载体，可以看做是画布，图片必须在画布的基础上进行创建<br>
2. axes<br>
   axes 表示绘图区域或者窗口，用来容纳一张具体的图片。axes 位于 figure 上，同一个 figure 上可以存在多个 axes。<br>
3. axis<br>
   axis 表示坐标轴，比如常见的 x 轴，y 轴以及对应的刻度线和标签。<br>
4. artist<br>
   atrist 表示广义的绘图元件，往大了说，figure, axes, axis 都属于绘图元件，往小了说，图片标题，图例，刻度，刻度标签等一幅图像上的具体元素都属于绘图元件。<br>

```
# 通过plt.subplots创建一个figure和axes对象，然后通过axes对象的各种方法来创建图表
import matplotlib.pyplot as plt
fig, ax = plt.subplots()
ax.plot([1, 2, 3, 4], [1, 2, 3, 4])
```

##### 绘图输出结果 backend

backend 可以分为两类：

1. 交互式设备，比如 qt,wxpython 等 GUI 窗口
   ![matplotlib输出1](https://github.com/chenhongyubio/chenhongyubio.github.io/raw/master/img/matplotlib输出1.png)<br>
2. 非交互式设备，比如 png, jpeg, pdf 等各种格式的文件
   ![matplotlib输出2](https://github.com/chenhongyubio/chenhongyubio.github.io/raw/master/img/matplotlib输出2.png)<br>

##### 修改内置 backend

```
# 修改配置文件matplotlibrc
import matplotlib
matplotlib.matplotlib_fname() # 找到配置文件位置
 # 修改backend值

# 设置环境变量
export  MPLBACKEND='agg'

# 绘图脚本的开头进行设置
import matplotlib
matplotlib.use('agg')
```

```
# 弹出对应结果
plt.show()  # 交互式图形设备
plt.savefig('out.png') # 非交互式图形设备
```

#### matplotlib 基础绘图命令之 plot

```
# plot命令主要用于绘制折线图
import matplotlib.pyplot ad plt
plt.plot([1,2,3,4],[1,2,3,4])
# 第一个参数的值作为x轴坐标，第二个参数的值作为y轴坐标
# 当只提供一个数值参数时，自动将其作为y轴坐标，x轴坐标为对应的数值下标
import pandas as pd
data_dict = pd.DataFrame({'xlabel':[1, 2, 3, 4], 'ylabel':[1, 2, 3, 4]})
plt.plot('xlabel', 'ylabel', data=data_dict)
```

```
# plot绘制散点图
import numpy as np
x = np.array([1, 2, 3, 4])
y = np.array([1, 2, 3, 4])
plt.plot(x,y,'o')  # 散点图
plt.plot(x,y,marker='o', linestyle='--', linewidth=2) # 散点图与直线图叠加
```

对于点而言，拥有以下基本属性

1. 填充色， markerfillcolor, 简写为 mec
2. 边框颜色，markeredgecolor, 简写为 mfc
3. 边框的线条宽度，markeredgewidth, 简写为 mfc
4. 大小, markersize, 简写为 ms
5. 形状, marker

对于线而言，用于以下基本属性

1. 颜色, color, 简写为 c
2. 宽度，linewidth, 简写为 lw
3. 风格，实线还是虚线，linestyle. 简写为 ls

![plot参数简写1](https://github.com/chenhongyubio/chenhongyubio.github.io/raw/master/img/plot参数简写1.png)<br>
![plot参数简写2](https://github.com/chenhongyubio/chenhongyubio.github.io/raw/master/img/plot参数简写2.png)<br>
![plot参数简写3](https://github.com/chenhongyubio/chenhongyubio.github.io/raw/master/img/plot参数简写3.png)<br>

```
# 图形叠加
plt.plot(x, y, label = 'sampleA')
plt.plot(x, y + 1, label = 'sampleB')
plt.plot(x, y + 2, label = 'sampleC')
plt.legend()
```

#### matplotlib 基础绘图命令之 bar

bar 命令用于绘制柱状图。

```
plt.bar(x = [1, 2, 3, 4], height = [4, 2, 3, 1])
```

参数 x 的值作为 x 轴坐标，height 的值作为 y 轴坐标。<br>

1. width, 柱子的宽度，即在 x 轴上的长度，默认是 0.8
2. color, 柱子的填充色
3. edgecolor, 柱子边框的颜色，默认为 None
4. linewidth, 柱子边框的宽度，默认为 0，表示没有边框
5. yerr,指定误差值的大小， 用于在柱子上添加误差线
6. ecolor, 表示 errorbar color, 误差线的颜色
7. bottom, 柱子底部的 baseline, 默认为 0

```
# 堆积柱状图
plt.bar(x = [1, 2, 3, 4], height = [4, 3, 2, 1], label = 'sampleA')
plt.bar(x = [1, 2, 3, 4], height = [4, 3, 2, 1], bottom = [4, 3, 2, 1], label = 'sampleB')
plt.legend()
# 核心是通过将第一组柱子的高度作为第二组柱子的底部，即bottom参数，从而实现堆积的效果
```

```
# 分组柱状图
width = 0.4
plt.bar(x = np.array([1, 2, 3, 4]) - width / 2, height = [4, 3, 2, 1], width = width, label = 'sampleA')
plt.bar(x = np.array([1, 2, 3, 4]) + width / 2, height = [1, 2, 3, 4], width = width, label = 'sampleB')
plt.legend()
# 核心是根据宽度的值，手动计算柱子的中心坐标，然后自然叠加就可以形成水平展开的分组柱状图
```

#### matplotlib 基础绘图命令之 pie

matplotlib 中，pie 方法用于绘制饼图。

```
plt.pie(x=[1, 2, 3, 4])
```

pie 方法常用的参数:<br>

1. labels, 设置饼图中每部分的标签<br>
2. autopct, 设置百分比信息的字符串格式化方式，默认值为 None,不显示百分比<br>
3. shadow, 设置饼图的阴影，使得看上去有立体感，默认值为 False<br>
4. startangle, 饼图中第一个部分的起始角度，<br>
5. radius, 饼图的半径，数值越大，饼图越大<br>
6. counterclock, 设置饼图的方向，默认为 True,表示逆时针方向，值为 False 时为顺时针方向<br>
7. colors，调色盘，默认值为 None, 会使用默认的调色盘，所以通常情况下，不需要设置该参数<br>
8. explode, 该参数用于突出显示饼图中的指定部分<br>

```
# 为了将图例和内容有效的区分开来，可以通过设置legend方法的bbox_to_anchor参数,
# 该参数用于设置图例区域在figure上的坐标，其值为4个元素的元组，分别表示x,y,width,height,
data=[1,2,3,4]
labels=['sampleA', 'sampleB', 'sampleC', 'sampleD']
plt.pie(x=data, labels=labels, autopct=lambda pct:'({:.1f}%)\n{:d}'.format(pct, int(pct/100 * sum(data))))
plt.legend(labels,loc="upper left",bbox_to_anchor=(1.2, 0, 0.5, 1))
```

#### matplotlib 基础绘图命令之 scatter

scatter 方法用于绘制散点图，与 plot 方法不同之处在于，scatter 主要用于绘制点的颜色和大小呈现梯度变化的散点图，也就是我们常说的气泡图。<br>

```
plt.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.randn(10))
# x和y参数指定x轴和y轴坐标，s参数指定mark size, 即点的大小，c参数指定color,即颜色。scatter会根据数值自动进行映射
# 难点在于其图例的处理上。scatter函数的返回值为一个PathCollections对象，通过其legend_elements方法，可以获得绘制图例所需的信息

scatter = plt.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.choice(np.arange(4), 10))
plt.legend(*scatter.legend_elements())

scatter = plt.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.choice(np.arange(4), 10))
plt.colorbar(scatter)

# legend_elements方法是有很多参数可以调整的，其中prop参数指定返回的信息，有两种取值，默认是colors, 表示返回的是点的颜色信息，取值为sizes时，返回的是点的大小信息。另外还有一个参数是num, 当图例的取值为连续型时，num指定了图例上展示的点的个数
scatter = plt.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.choice(np.arange(4), 10))
plt.legend(*scatter.legend_elements(prop='sizes', num = 6))

# 组合图例
fig, ax = plt.subplots()
scatter = ax.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.choice(np.arange(4), 10))
legend1 = ax.legend(*scatter.legend_elements(prop='colors'), loc='upper left',title='colors',bbox_to_anchor=(1, 0, 0.5, 1))
ax.add_artist(legend1)
legend2 = ax.legend(*scatter.legend_elements(prop='sizes', num = 6), loc='lower left',title='sizes',bbox_to_anchor=(1, 0, 0.5, 1))
```

#### matplotlib 基础绘图命令之 errorbar

在 matplotlib 中，errorbar 方法用于绘制带误差线的折线图。<br>

```
plt.errorbar(x=[1, 2, 3, 4], y=[1, 2, 3, 4], yerr=1)
# yerr参数用于指定y轴水平的误差，同时该方法也支持x轴水平的误差，对应参数xerr。指定误差值有多种方式，上述代码展示的是指定一个统一标量的用法，此时，所以的点误差值都一样。
plt.errorbar(x=[1, 2, 3, 4], y=[1, 2, 3, 4], yerr=[1, 2, 3, 4]) # 不同误差线
plt.errorbar(x=[1, 2, 3, 4], y=[1, 2, 3, 4], yerr=[[1,2,3,4],[1, 2, 3, 4]]) # 每个点上下误差不一样
```

```
# 样式更改
# fmt参数的值和plot方法中指定点的颜色，形状，线条风格的缩写方式相同
plt.errorbar(x=[1, 2, 3, 4], y=[1, 2, 3, 4], yerr=1, fmt='co--')
# ecolor参数指定error bar的颜色，可以和折线的颜色加以区分
plt.errorbar(x=[1, 2, 3, 4], y=[1, 2, 3, 4], yerr=1, fmt='co--', ecolor='g')
# elinewidth参数指定error bar的线条宽度
plt.errorbar(x=[1, 2, 3, 4], y=[1, 2, 3, 4], yerr=1, fmt='ro-',ecolor='k',elinewidth=10)

# lims系列参数
# lims系列参数用于控制误差线的显示，对于x轴水平的误差线而言，有以下两个参数
# 1. xuplims
# 2. xlolims
# 对于y轴水平的误差线而言，有以下两个参数
# 1. uplims
# 2. lolims
# 默认的取值为False， 当取值为True时，对应方向的误差线不显示，同时在另外一个方向上的误差线上，会用箭头加以标识。
plt.errorbar(x=[1, 2, 3, 4], y=[1, 2, 3, 4], yerr=1, uplims=True)
plt.errorbar(x=[1, 2, 3, 4], y=[1, 2, 3, 4], yerr=1, lolims=True)
plt.errorbar(x=[1, 2, 3, 4], y=[1, 2, 3, 4], yerr=1, uplims=True, lolims=True)

# errorevery参数用于指定误差线的抽样频率，默认情况下，每个点的误差线都会显示，当点很多且密集分布时, 每个点都显示误差线的话，就很难看出有效的信息，
plt.errorbar(x=range(100), y=range(100),yerr=50)
plt.errorbar(x=range(100), y=range(100),yerr=50,errorevery=6) # 使用errorevery参数进行抽样

# 样式精细调整
plt.errorbar(x=[1, 2, 3, 4], y=[1, 2, 3, 4], yerr=1, marker='s', mfc='red', mec='green', ms=20, mew=4)
```

#### 一文搞懂 matplotlib 中的颜色设置

##### 常用颜色的字母表示及缩写

```
1. red,表示红色,  简写为r
2. green, 表示绿色，简写为g
3. blue,表示蓝色，简写为b
4. yellow,表示黄色，简写为y
5. cyan,表示蓝绿色，简写为c
6. magenta,表示粉紫色，简写为m
7. black,表示黑色，简写为k
8. white,表示白色，简写为w
```

##### T10 调色盘

在 matplotlib 中，默认的颜色盘通过**参数 rcParams["axes.prop_cycle"]参数**来指定, 初始的调色盘就是 T10 调色盘。<br>
T10 调色盘适用于离散分类，其颜色名称以 tab:为前缀。<br>
在 matplotlib 中，默认就是通过这个 T10 调色盘来个不同的 label 上色的。<br>

```
1. tab:blue
2. tab:orange
3. tab:green
4. tab:red
5. tab:purple
6. tab:brown
7. tab:pink
8. tab:gray
9. tab:olive
10. tab:cyan
```

##### CN 式写法

CN 式写法以字母 C 为前缀，后面加从 0 开始的数字索引，其索引的对象为 rcParams["axes.prop_cycle"]指定的调色盘。CN 式对应调色板，当切换调色板时，CN 也会对应改变<br>

##### xkcd 颜色名称

在 matplotlib 中，通过 xkcd:前缀加对应的颜色名称进行使用，而且是不区分大小写的。具体网站为：https://xkcd.com/color/rgb/ <br>

##### X11/CSS4 颜色名称

```
# 通过字典查看颜色
import matplotlib._color_data as mcd
for key in mcd.CSS4_COLORS:
    print('{}: {}'.format(key, mcd.CSS4_COLORS[key]))
```

##### 十六进制颜色代码

```
# 十六进制的颜色代码可以精确的指定颜色，在matplotlib中也支持
plt.pie(x=[1,2,3,4], colors=['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728'])
```

##### RGB/RGBA 元组

```
# 所有的颜色都是有RGB三原色构成，在matplotlib中，可以通过一个元组来表示表示red, green, blue三原色的比例，以及一个可选的alpha值来表示透明度，取值范围都是0到1
plt.pie(x=[1,2,3,4], colors=[(0.1, 0.2, 0.5),(0.1, 0.3, 0.5),(0.1, 0.4, 0.5),(0.1, 0.5, 0.5)])
```

##### 灰度颜色

```
# 在matplotlib中，通过0到1之间的浮点数来对应灰度梯度，在使用时，为了有效区分，需要通过引号将其装换为字符
plt.pie(x=[1,2,3,4], colors=['0','0.25', '0.5', '0.75'])
```

#### matplotlib 基础绘图命令之 hist

hist 方法用于绘制直方图。<br>

```
plt.hist(x = np.random.normal(size=1000))
```

具体参数：<br>

1. bins,控制直方图中的区间个数
2. color,指定柱子的填充色
3. edgecolor, 指定柱子边框的颜色
4. density,指定柱子高度对应的信息，有数值和频率两种选择
5. orientation，指定柱子的方向，有水平(horizontal)和垂直(vertical)两个方向
6. histtype，绘图的类型 bar、step

#### matplotlib 基础绘图命令之 boxplot

```
plt.boxplot(x=np.random.normal(size=1000))
```

具体参数：<br>

1. notch,控制箱体图的形状,控制是否在图中显示中位数的置信区间(True)
2. sym, 控制离群点的样式
3. vert,控制箱体的方向,True 竖直，False 水平
4. patch_artist，进行箱体图的颜色填充
5. showmeans，显示均值
6. labels, 指定 x 轴的坐标
   boxplot 的返回值是一个字典,包括了箱体图中的各个元素<br>
7. whiskers, 对应箱体图中箱体上下两侧竖直的线条
8. caps, 对应箱体图中竖直线条端点的水平线段
9. boxes, 对应箱体图中的主体方框
10. medians,对应箱体图中的中位数线段
11. fiers,对应箱体图中的离群点
12. means,对应箱体图中表示均值的点

#### matplotlib 基础绘图命令之 violinplot

```
plt.violinplot(dataset=np.random.normal(size=1000))
```

具体参数：<br>

1. vert,控制图形的方向
2. showmeans, 是否在图中显示均值
3. showmedians,是否在图中显示中位数
4. showextrema, 是否在图中显示最大值和最小值

```
np.random.seed(19680801)
data = [np.random.normal(size=500), np.random.normal(size=1000)]
violin = plt.violinplot(dataset=data, showextrema=False)
for patch in violin['bodies']:
    patch.set_facecolor('#D43F3A')
    patch.set_edgecolor('black')
    patch.set_alpha(1)
for i,d in enumerate(data):
    min_value,quantile1, median, quantile3, max_value = np.percentile(d, [0, 25, 50, 75, 100])
    print(median)
    plt.scatter(i+1, median, color='white',zorder=4)
    plt.vlines(i+1,quantile1, quantile3, lw=9, zorder=3)
    plt.vlines(i+1,min_value, max_value, zorder=2)
plt.xticks(ticks=[1,2], labels=['A', 'B'])
```

#### matplotlib 基础绘图命令之 imshow

imshow 方法用于绘制热图。<br>
imshow 方法首先将二维数组的值标准化为 0 到 1 之间的值，然后根据指定的渐变色依次赋予每个单元格对应的颜色，就形成了热图。<br>

```
plt.imshow(data)
plt.colorbar()  # 图例
```

1. cmap：指定渐变色，完整的内置 colormap 列表https://matplotlib.org/tutorials/colors/colormaps.html
2. aspect：指定热图的单元格的大小，equal/auto
3. alpha：指定透明度
4. origin：指定绘制热图时的方向 upper/lower
5. vmin 和 vmax：用于限定数值的范围
6. interprolation：控制热图的显示形式 None/none/nearest/bilinear/bicubic
7. extent：指定热图 x 轴和 y 轴的极值,前两个数值对应 x 轴的最小值和最大值，后两个参数对应 y 轴的最小值和最大值

#### 渐变色

1. sequential
   1. perceptually uniform sequential colormaps
   2. sequential colormaps
   3. sequential2 colormaps
2. diverging
3. cyclic
4. qualitative

##### 自定义渐变色

1. ListedColormap
2. LinearSegmentedColormap

#### 掌握坐标轴的 log 转换

对于跨度很大其分布离散的数据，常用 log 转换来缩写其差距。<br>

1. loglog, 同时对 x 轴和 y 轴的值进行 log 转换
2. semilogx, 只对 x 轴的值进行 log 转换，y 轴的值不变
3. semilogy, 只对 y 轴的值进行 log 转换，x 轴的值不变

专属参数：<br>

1. base, 指定对数的值，默认值为 10，即进行 log10 的转换
2. subs，设定 minor ticks 的位置，默认值为 None
3. nonpositive, 对非负值的处理，因为只有正数可以取 log, 如果原始值为负值，此时有两种处理方式，第一种是丢掉这个点，也是默认的处理方式，对应该参数的值为 mask, 在图中不显示这个点，第二种是将这个值调整为最接近的正数，对应该参数的取值为 clip

#### 点线图和阶梯图

在 matplotlib 中，通过 step 函数来实现折线图。<br>

```
import matplotlib.pyplot as plt
x = range(20)
y = range(20)
plt.step(x, y)
# where参数用于控制阶梯的样式
# pre,post,mid：指定折线位置
```

点线图在 matplotllib 中通过 stem 函数来实现。<br>

```
plt.stem(x, y)
# markerfmt, linefmt, basefmt3个参数来控制其外观
```

#### 数据添加置信区间

在 matplotlib 中， 可以通过 fill_between 系列函数来实现图中的置信区间的展示效果。<br>
该系列包含了 fill_between 和 fill_betweenx 两个函数，其中，fill_between 函数用于在两个水平曲线之间进行填充，fill_betweenx 用于在两条数值区间之间进行填充, 两个函数的参数完全一致。<br>
fill_between 函数有 x, y1, y2 这 3 个基本参数，其中通过(x, y1)指定了第一条水平线，（x, y2）指定了第二条水平线，然后在两个水平线之间进行填充。其中，y2 参数是有默认值的，其默认值为 0。<br>
[为你的数据添加置信区间](https://mp.weixin.qq.com/s/LzVGIh4118JsRdUfMIINNQ)

#### 添加直线的两种方式

在 matplotlib 中, hlines 用于绘制水平线，vlines 用于绘制垂直线，二者的用法相同，都需要 3 个基本参数。<br>
hlines 和 vlines 系列函数一次可以绘制多条直线，而且可以根据起始和结束坐标，灵活指定直线的跨度。
axhline 和 axvline 系列函数一次只可以添加一条直线。<br>
axhine 和 axvline 基于绘图区域百分比的形式添加直线，hlines 和 vlines 函数则基于坐标的方式灵活指定直线的范围.<br>

#### 绘制双坐标图

在 matplotlib 中存在两种方式来实现双坐标图：

1. secondary_axis 系列函数：secondary_axis,secondary_yaxis
   第一个参数用于指定第二个坐标轴的位置，双 Y 轴取值为 left/right,双 X 轴取值为 top/bottom，也可取值为 0，1 以及小数
   第二个参数用于指定第二个坐标轴的 scale，值为长度为 2 的元组
2. twin 系列函数：twinx 和 twiny

#### 对图标的坐标轴进行调整

针对坐标轴各个元素的个性化调整，matplotlib 存在对应的函数。<br>

##### 标题

1. set_xlabel，设置 x 轴的标题
2. set_ylabel，设置 y 轴的标题
3. set_title，设置图片标题

##### 刻度线

1. set_xticks，设置 x 轴的刻度（get_xticks 获取刻度线）
2. set_yticks，设置 y 轴的刻度（get_yticks 获取刻度线）

##### 刻度线标签

1. set_xticklabels，设置 x 轴刻度线标签（get_xticklabels 获取刻度线标签）
2. set_yticklabels，设置 y 轴刻度线标签（get_yticklabels 获取刻度线标签）

##### 坐标轴范围

1. set_xlim 或 set_xbound, 设置 x 轴的坐标范围（get_xlim/xbound 获取刻度线范围）
2. set_ylim 或 set_ybound, 设置 y 轴的坐标范围（get_xlim/xbound 获取刻度线范围）

##### 坐标轴反转(坐标轴逆向显示)

1. invert_xaxis，逆向 x 轴（ax.xaxis_inverted() 检查是否反转）
2. invert_yaxis，逆向 y 轴（ax.yaxis_inverted() 检查是否反转）

##### 综合性函数

ax.tick_params(direction='in',bottom=False,top=True,labeltop=True,labelbottom=False) <br>
direction 参数控制刻度线的方向，bottom 和 top 控制对应方向的刻度线是否显示，labelbottom 和 labeltop 控制对应放下的刻度线标签是否显示.<br>

#### 个性化调整坐标轴

matplotlib 中对于坐标轴轴线的调整需要采用 spines 对象来实现。此外还可以使用 set_visiable 方法<br>

```
ax.spines['top'].set_color(None)
ax.spines['right'].set_color(None)
# 图像的上下左右四个边框分别对应spines的top, bottom, left, right4个key的值，将其颜色设置为None,就可以起到隐藏对应边框的作用
ax.spines['top'].set_visible(False)
ax.spines['right'].set_visible(False)
```

通过 axes 的 spine 属性可以方便的调整坐标轴轴线的属性。<br>

```
ax.spines['right'].set_color(None)
ax.spines['top'].set_color(None)
ax.spines['left'].set_position('center')
ax.spines['bottom'].set_position('center')
```

#### 实现一页多图

matplotlib 中存在两种方式实现一页多图(拼图)，一是直接指定，二是动态增加。直接指定是在创建 figure 的时候，就直接定义好多个 axes 的排列方式；动态增加则是根据需要在 figure 上添加 axes。

```
# 直接指定可以通过pyplot子模块的subplots函数来实现
fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2)
ax1.plot([1,2,3,4])
ax2.bar(x = [1, 2, 3, 4], height = [4, 2, 3, 1])
ax3.hist(x = np.random.normal(size=1000), bins=50)
ax4.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.randn(10))
plt.show()

# 动态指定是在生成新的axes对象的同时，指定其排列的位置，通过pyplot子模块的subplot函数来实现
# 前两个数字分别表示布局的行数和列数，第三个数值表示的是索引
ax1 = plt.subplot(221)
ax2 = plt.subplot(222)
ax3 = plt.subplot(223)
ax4 = plt.subplot(224)

ax1.plot([1,2,3,4])
ax2.bar(x = [1, 2, 3, 4], height = [4, 2, 3, 1])
ax3.hist(x = np.random.normal(size=1000), bins=50)
ax4.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.randn(10))
plt.show()

# 支持不同axes占据不同区域，通过pyplot子模块的subplot2grid函数来实现
# 第一个元组表示布局的行数和列数，第二个元组表示axes的数组下标，colspan和rowspan分别指定该axes占据的行数和列数。
ax1 = plt.subplot2grid((3, 3), (0, 0), colspan=2)
ax2 = plt.subplot2grid((3, 3), (1, 0), colspan=2, rowspan=2)
ax3 = plt.subplot2grid((3, 3), (1, 2), rowspan=2)
ax1.bar(x = [1, 2, 3, 4], height = [4, 2, 3, 1])
ax2.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.randn(10))
ax3.hist(x = np.random.normal(size=1000), bins=50)
plt.show()

# 将figure视为左下角为(0,0), 右上角为(1, 1)的坐标系，通过left等参数分别指定上下左右的坐标，从而设置绘图区域的大小。wspace和hspace参数分别指定分割线的宽度和高度，其数值为每个axes width和height的比例。
plt.subplots_adjust(left=0.25, right=0.9, bottom=0.1, top=0.9, wspace=0.2, hspace=0.2)
```

#### 画中画

matplotlib 实现画中画的方式有两种。<br>

```
# 第一种：通过在原本axes中插入一个新的axes, 来实现画中画的目的
fig,ax = plt.subplots()
ax.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.randn(10))
ax1 = ax.inset_axes([0.6, 0.5, 0.3, 0.45])  # 插入新的axes
ax1.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.randn(10))
plt.show()

# 第二种：对图中的局部区域进行缩放，属于画中画的一种特殊情况
# indicate_inset_zoom
fig,ax = plt.subplots()
seed = 123456
np.random.seed(seed)
ax.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.randn(10))
ax1 = ax.inset_axes([0.6, 0.5, 0.32, 0.45])
np.random.seed(seed)
ax1.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.randn(10))
ax1.set_xlim(-1.5, -0.8)
ax1.set_ylim(-0.8, -0.3)
ax.indicate_inset_zoom(ax1)
plt.show()
```

#### 设置不同主题

主题就是指对背景色，坐标轴，标题等元素进行设定。在 matplotlib 中通过 matplotlib.style 模块进行定义。

```
# 查看所有主题
plt.style.available

# 基本用法
import numpy as np
import matplotlib.pyplot as plt
plt.style.use('dark_background')
plt.plot(np.sin(np.linspace(0, 2 * np.pi)), 'r-o')
plt.show()

# 查看主题的具体定义
import matplotlib
import matplotlib.style
print(matplotlib.style.library['dark_background'])

# 主题中定义修改--rcParams字典实现
import numpy as np
import matplotlib as mpl
import matplotlib.pyplot as plt
plt.style.use('ggplot')
mpl.rcParams['xtick.color'] = 'red'
mpl.rcParams['ytick.color'] = 'blue'
plt.plot(np.sin(np.linspace(0, 2 * np.pi)), 'r-o')
plt.show()

# 自定义主题
# 进入matplotlib安装路径下的stylelib文件夹
# 构建自己的主题文件即可
```

#### 通过 cycler 实现属性的自动映射

这里提到的属性映与 R 语言 ggplot 中的概念其实是一致的。<br>

```
import matplotlib.pyplot as plt
import numpy as np
x = np.linspace(0, 3 * np.pi, 50)
offsets = np.linspace(0, 2 * np.pi, 4, endpoint=False)
for i in range(6):
     y = np.sin(x) + i
     plt.plot(x, y)
plt.show()

matplotlib.rcParams['axes.prop_cycle']  # axes.prop_cycle属性设置颜色的自动映射，超出数量时会自动循环
```

```
# 通过cyler模块，可以自定义这样的属性循环
from cycler import cycler
custom_cycler = cycler(color=['c', 'm', 'y', 'k'])
fig, ax = plt.subplots()
ax.set_prop_cycle(custom_cycler)   # set_prop_cycle将该颜色循环添加到特定的axes对象上
x = np.linspace(0, 3 * np.pi, 50)
offsets = np.linspace(0, 2 * np.pi, 4, endpoint=False)
for i in range(6):
 y = np.sin(x) + i
 ax.plot(x, y)
plt.show()

# 该循环可以定义的属性很多，颜色，线条宽度，线条样式等常用属性都可以进行定义，而且不同的循环还可以进行叠加
from cycler import cycler
custom_cycler = cycler(cycler(color=['c', 'm', 'y']) + cycler(linestyle=['-', '--', ':']))
fig, ax = plt.subplots()
ax.set_prop_cycle(custom_cycler)
x = np.linspace(0, 3 * np.pi, 50)
offsets = np.linspace(0, 2 * np.pi, 4, endpoint=False)
for i in range(6):
... y = np.sin(x) + i
... ax.plot(x, y)
plt.show()
```

#### 添加图例

存在两种添加图例的方式：

1. 在绘制元素时指定 label,然后 legend 自动识别对应的 label 属性，绘制图例
2. 绘制元素时不需要指定 label, 但是需要获取对应的 artist 对象，然后在 legend 函数中为其指定对应的 label

```
# 第一种方法
>>> x = np.linspace(0, 2 * np.pi, 50)
>>> plt.plot(x, np.sin(x), label='sin')
>>> plt.plot(x, np.cos(x), label='cos')
>>> plt.legend()
>>> plt.show()
`
# 第二种方法
>>> x = np.linspace(0, 2 * np.pi, 50)
>>> line1, = plt.plot(x, np.sin(x))
>>> line2, = plt.plot(x, np.cos(x))
>>> plt.legend((line1, line2), ('sin', 'cos'))
>>> plt.show()

# 位置属性
plt.legend(['sin'], loc='upper center')    # 字符串设置
plt.legend(['sin'], loc=(0.65, 0.75))   # 坐标设置

# legend函数存在两种方法，axes.legend 和 figure.legend，默认调用前者
```

#### constrained 和 tight layout

constrained 和 tight layout 主要在 matplotlib 中进行图片自动调整，如超出边框显示不全等等。<br>

```
plt.subplots(constrained_layout=True)
plt.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.randn(10))
plt.title('title', fontsize = 60)
plt.xlabel('xlabel', fontsize = 30)
plt.ylabel('ylabel', fontsize = 30)
plt.show()

plt.scatter(x= np.random.randn(10), y=np.random.randn(10),s=40 * np.arange(10),c=np.random.randn(10))
plt.title('title', fontsize = 60)
plt.xlabel('xlabel', fontsize = 30)
plt.ylabel('ylabel', fontsize = 30)
plt.tight_layout()
plt.show()
```

#### 用不同的坐标系统对图形元素进行定位

matplotlib 中常用的坐标系统：

1. data，其实就是最常用的 x 轴和 y 轴了，通过指定 xlim 和 ylim 范围内的数值来指定元素的位置，
2. axes,将 axes 的左下角视为(0, 0), 右上角视为(1,1),从而对元素进行定位
3. figure, 将 figure 的左下角视为(0, 0), 右上角视为(1,1),从而对元素进行定位

通过 transform 参数，可以显式指定坐标系统。<br>

#### 三维图绘制

通过 mplot3d 工具可以实现，只需要在 axes 对象中指定 projection 参数为 3d 即可，只需要同时提供 x,y,z 三个坐标轴对应的值即可。<br>

```
fig = plt.figure()
ax = plt.axes(projection='3d')
```

#### 设置坐标轴刻度的位置和样式

在 matplotlib 中，通过子模块 ticker 可以对坐标轴刻度的位置和样式进行设置。<br>

1.  set_major_locator
2.  set_minor_locator
3.  set_major_formatter
4.  set_minor_formatter
    多种设置方式<br>
    locator 形式<br>
5.  AutoLocator, 默认值，自动对刻度线的位置进行设置
6.  MaxNLocator, 根据提供的刻度线的最大个数，自动设置
7.  IndexLocator, 根据起始位置和间隔来设置刻度线
8.  MultipleLocator, 根据指定的间隔来设置刻度线
9.  FixedLocator, 根据提供的列表元素来设置刻度线
10. NullLocator,不显示刻度线
    formatter 形式<br>
11. PercentFormatter，标签显示成百分比
12. StrMethodFormatter，根据字符串格式化语法进行格式化
13. FormatStrFormatter，根据字符串格式化语法进行格式化
14. MultipleLocator, 根据指定的间隔来设置刻度线
15. NullFormatter，不显示标签

#### 图中添加多边形

在 matplotlib 中有一个子模块 patches, 提供了绘制各种多边形的功能 <br>

```
# 圆形
patch = patches.Circle((0.5, 0.5), radius=0.2, transform=ax.transAxes)
# 椭圆
patch = patches.Ellipse((0.5, 0.5), width=0.4, height= 0.2)
# 箭头
patch = patches.Arrow(x=0.2, y=0.2, dx=0.5, dy=0.6)
# 矩形
patch = patches.Rectangle(xy=(0.2,0.2), width=0.5, height=0.4)
# 多边形
patch = patches.Polygon(np.array(([0.2, 0.2], [0.4, 0.6], [0.6, 0.2])))
# 连线
patch = patches.ConnectionPatch(xyA=(0.2, 0.2), xyB=(0.8, 0.8), coordsA=ax.transData, coordsB=ax.transData)
# 曲线
style = patches.ConnectionStyle.Arc3(rad=0.2)
patch = patches.ConnectionPatch(xyA=(0.2, 0.2), xyB=(0.8, 0.8), coordsA=ax.transData, coordsB=ax.transData,connectionstyle=style)
# 自定义多边形
# 通过子模块path可以自定义形状
from matplotlib.path import Path
fig, ax = plt.subplots(figsize=(4,4))
verts = [(0.2, 0.2),(0.2, 0.6),(0.5,0.8),(0.8,0.6),(0.8,0.2)]
codes = [Path.MOVETO, Path.LINETO, Path.LINETO, Path.LINETO, Path.LINETO]
path = Path(verts, codes)
patch = patches.PathPatch(path)
ax.add_artist(patch)
plt.show()
# 对于单个多边形而言，通过add_artist方法添加到axes上，如果需要绘制多个多边形，可以通过绘制PatchCollection来一次性添加多个
```

#### 极坐标系

```
import numpy as np
import matplotlib.pyplot as plt
r = np.arange(0, 2, 0.01)
theta = 2 * np.pi * r
ax = plt.subplot(111, projection='polar')   # projection参数定义极坐标系
ax.plot(theta, r)
ax.set_rticks([0.5, 1, 1.5, 2])
plt.show()
```

在 matplotlib 的极坐标系中，确定点的坐标需要两个值，第一个值是点的弧度值，第二个是半径，简单理解，弧度看做是笛卡尔坐标系中的 x 轴坐标，半径看做是笛卡尔坐标系中的 y 轴坐标。<br>

```
vals = [123, 124, 102, 111, 100, 121, 96, 107, 111, 116, 101, 83, 91, 123, 109, 130, 125, 87, 91, 99, 115, 109, 123, 111]
theta = np.linspace(0, 2 * np.pi, len(vals))
ax = plt.subplot(111, projection='polar')
ax.bar(theta, vals, width = 2 * np.pi / len(vals))
ax.tick_params(labelleft=False)
plt.show()

# 显示部分区域
vals = [123, 124, 102, 111, 100, 121, 96, 107, 111, 116, 101, 83, 91, 123, 109, 130, 125, 87, 91, 99, 115, 109, 123, 111]
theta = np.linspace(0, 2 * np.pi, len(vals))
ax = plt.subplot(111, projection='polar')
ax.bar(theta, vals, width = 2 * np.pi / len(vals))
ax.tick_params(labelleft=False)
ax.set_thetamin(45)
ax.set_thetamax(135)
plt.show()

# 设置半径范围
vals = [123, 124, 102, 111, 100, 121, 96, 107, 111, 116, 101, 83, 91, 123, 109, 130, 125, 87, 91, 99, 115, 109, 123, 111]
theta = np.linspace(0, 2 * np.pi, len(vals))
ax = plt.subplot(111, projection='polar')
ax.bar(theta, vals, width = 2 * np.pi / len(vals))
ax.tick_params(labelleft=False)
ax.set_rorigin(-20)
plt.show()
```

#### 多图排版技巧

```
# 在matplotlib中，可以通过ImageGrid方法来调节多图的排版问题
# single只显示一个图例
fig = plt.figure()
grid = ImageGrid(fig, rect=(0.05,0.05,0.8,0.8),nrows_ncols=(1, 2), axes_pad=0.25, label_mode="1", cbar_location="right", cbar_mode="single")
for ax in grid:
... im = ax.imshow(data)
grid.cbar_axes[0].colorbar(im)
plt.show()

# each每幅图对应自己的图例
fig = plt.figure()
grid = ImageGrid(fig, rect=(0.05,0.05,0.8,0.8),nrows_ncols=(1, 2), axes_pad=0.5, label_mode="1", cbar_location="right", cbar_mode="each", cbar_pad="3%")
for ax, cax in zip(grid, grid.cbar_axes):
    im = ax.imshow(data)
   cax.colorbar(im)
plt.show()

# 图片大小不一致设置
data1 = np.random.rand(50).reshape(5, 10)
data2 = np.random.rand(30).reshape(5, 6)
data3 = np.random.rand(20).reshape(5, 4)
fig = plt.figure()
grid = ImageGrid(fig, rect=(0.05,0.05,0.8,0.8),nrows_ncols=(1, 3), axes_pad=0.25, label_mode="1", cbar_location="right", cbar_mode="single", cbar_pad="3%")
for ax, data in zip(grid, [data1, data2, data3]):
   im = ax.imshow(data)
grid.cbar_axes[0].colorbar(im)
plt.show()
```

#### seaborn 更高效的统计图表制作工具

seaborn 是针对数据的统计学描述，整合了一系列相关的可视化功能。<br>

1. relplot, 描述数据点之前的关联，可视化形式是散点图和折线图
2. displot, 描述数据点的分布，可视化形式包括直方图，密度曲线等
3. catplot, 描述分类变量的分布，可视化形式包括箱体图，柱状图，小提琴图等

```
import seaborn as sns
sns.relplot(data=df, x='total_bill', y='tip', kind='scatter')
# 使用relplot函数来可视化x和y变量的关系，kind参数的值为scatter
sns.scatterplot(data=df, x='total_bill', y='tip')
```

##### 属性映射

```
# hue参数用于映射颜色属性，style颜色用于映射形状属性，size参数用于映射点的大小属性
sns.relplot(data=df, x='total_bill', y='tip', hue='day', style='day')
```

##### 分面

```
# 通过row和col参数将数据框的列映射为不同的分面,仅在大类函数中适用
sns.relplot(data=df, x='total_bill', y='tip', hue='day', col='time')
```

```
# pairplot
sns.pairplot(df)
# jointplot
sns.jointplot(data=df, x='total_bill', y='tip', hue='day')
```

#### seaborn 之折线图和散点图关联

在 seaborn 中，satterplot 绘制散点图，lineplot 绘制折线图。<br>

1. hue, 用于映射颜色
2. size, 于映射线条的宽度或者点的大小
3. style, 用于映射线条的样式或者点的样式

```
# 散点图绘制
df = pd.read_csv('tips.csv')
sns.scatterplot(data=df, x="total_bill", y="tip", hue="day", style="time", size="size")
plt.show()

# 折线图绘制
sns.lineplot(data=df, x="total_bill", y="tip", hue="day", style="time", size='size')

# 属性映射顺序
# 1. hue_order（针对离散变量）
# 2. size_order
# 3. style_order
sns.scatterplot(data=df, x="total_bill", y="tip", hue="day", style="time", size='size', hue_order=['Fri','Thur','Sat','Sun'])

# norm系列函数用于映射连续变量的映射过程
sns.scatterplot(data=df, x="total_bill", y="tip", hue="size", style="time", hue_norm=(2, 5))

# 属性组合
sns.scatterplot(data=df, x="total_bill", y="tip", hue="day", style="day")

# 分面
sns.relplot(data=df, x="total_bill", y="tip", hue="day", col="time")
```

#### seaborn 数据总体分布可视化

1. histplot. 通过直方图来展示数据分布
2. kdeplot, 通过密度分布图来展示数据分布
3. ecdfplot. 通过累积分布曲线来展示数据分布
4. rugplot. 通过 x 轴和 y 轴的边际分布来展示数据分布

#### seaborn 分类变量的汇总展示

根据分类变量对样本进行分组，然后展示每一组的分布，适合多组数据的横向比较。<br>

1. stripplot,
2. swarmplot
3. boxplot
4. violinplot
5. boxenplot
6. pointplot
7. barplot
8. countplot

#### seaborn 可视化数据库中多个列元素

seaborn 中 pairplot 函数用于快速展示列元素分布和相互关系的函数。该函数会自动选取数据框中值为数字的列元素，其中对角线用于展示各个列元素的分布情况，剩余空间展示每两个列元素之间的关系。<br>

```
df = pd.read_csv("text.csv")
sns.pairplot(df)
plt.show()

# 通过corner参数，可以控制只显示图形的一半
sns.pairplot(df,corner=True)
plt.snow()

# kind和diag_kind用于指定上下三角区域和对角线区域的可视化方式
sns.pairplot(df, kind='reg', diag_kind='kde')
plt.show()

# x_vars和y_vars指定列
sns.pairplot(df, x_vars=['bill_length_mm', 'bill_depth_mm'], y_vars=['bill_length_mm', 'bill_depth_mm'])
plt.show()

# hue用于分组变量的颜色映射
sns.pairplot(df,hue="species")
plt.show()
```

#### seaborn 绘制热图

```
# heatmap绘制普通热图
sns.heatmap(data)
plt.show()
sns.heatmap(data, linewidth=1)
plt.show()
sns.heatmap(data, linewidth=1, annot=True)
plt.show()

# clustermap绘制带聚类数的热图
sns.clustermap(df)
plt.show()
sns.clustermap(df, standard_scale=0)  # 按行进行数据标准化
plt.show()
sns.clustermap(df, z_score=0)  # 按行zscore标准化
plt.show()
sns.clustermap(df, col_colors=['r','g','b','b','b'])  # 对行标签和列标签进行注释
plt.show()
```

#### seaborn中jointplot探究两组变量分布及关系
```
# 同时绘制两组变量的散点图以及各自对应的直方图
sns.jointplot(data=df, x='bill_length_mm', y='bill_depth_mm')
plt.show()

# kind参数调整可视化形式
# reg/hist/kde/hex/resid
# plot_joint函数用于指定x和y相互关系的可视化形式，plot_marginals函数用于指定x和y变量各自分布的可视化形式。结合jointplot一起使用时，是在已有可视化元素的基础上进行添加，可以通过zorder等参数指定优先级。

# JointGrid灵活接口
g = sns.JointGrid(data=df, x='bill_length_mm', y='bill_depth_mm')
g.plot(sns.scatterplot, sns.histplot)
plt.show()
```

#### seaborn绘图风格的设置
```
# context
sns.plotting_context()    # 查看context影响的具体元素
sns.set_context('notebook')     # 设置对应的context值

# style
sns.axes_style("white")     # 查看对应的元素属性
with sns.axes_style('white'):
...     sns.scatterplot(data=df, x='total_bill', y='tip')
plt.show()
sns.set_style('white', rc={'figure.facecolor':'black'})   # 修改部分属性的值

# theme
#  一次性设置context, style, palette等属性
sns.set_theme(context='notebook', style='darkgrid', palette='deep', font='sans-serif')
sns.set(context='notebook', style='darkgrid', palette='deep', font='sans-serif')   # set为set_theme别名

```

#### seaborn颜色设置
```
# 通过color_palette函数来设置颜色
sns.color_palette()

# 存在多种颜色梯度
palettes = ['deep', 'muted', 'pastel', 'bright', 'dark', 'colorblind']
ax.pie(x, colors = sns.color_palette(palette))

# 借用matplotlib颜色列表
plt.pie(x, colors=sns.color_palette('Paired'))

# 通过色相、饱和度和明度来设置颜色
# 通过husl_palette和hsl_palette两个子函数来实现
fig, (ax1, ax2) = plt.subplots(1, 2)
ax1.pie(x, colors=sns.color_palette('husl', 10))
ax1.text(0.5, 1, 'husl', transform=ax1.transAxes, ha='center')
ax2.pie(x, colors=sns.color_palette('hls', 10))
ax2.text(0.5, 1, 'hls', transform=ax2.transAxes, ha='center')
plt.show()

# 通过子函数cubehelix_palette来实现
plt.pie(x, colors=sns.color_palette('ch:')) # 通过前缀ch:来标识对应的参数
plt.show()

# light, dark and blend  palette
fig, (ax1, ax2, ax3) = plt.subplots(1, 3)
ax1.pie(x, colors=sns.color_palette('light:blue'))
ax1.text(0.5, 1, 'light_palette', transform=ax1.transAxes, ha='center')
ax2.pie(x, colors=sns.color_palette('dark:blue'))
ax2.text(0.5, 1, 'dark_palette', transform=ax2.transAxes, ha='center')
ax3.pie(x, colors=sns.color_palette('blend:red,blue'))
ax3.text(0.5, 1, 'blend_palette', transform=ax3.transAxes, ha='center')
plt.show()

# 自定义颜色
plt.pie(x, colors=sns.color_palette(['xkcd:green','xkcd:blue','xkcd:red', 'xkcd:brown', 'xkcd:pink', 'xkcd:purple'])）
plt.show()

# 绘制热图渐变色
# rocket
# flare
# mako
# crest
sns.heatmap(data, cmap='rocket')
```