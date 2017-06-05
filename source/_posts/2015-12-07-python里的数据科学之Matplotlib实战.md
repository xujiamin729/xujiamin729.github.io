---
layout:		post
title:		Python里的数据科学之matplotlib实战
categories:
- TECHNOLOGY
tags:
- Python
- ML
- Plt
permalink:  Explore-matplotlib-Python
comments:	true
date:		2015-12-07 13:46:20
---
这篇和Numpy类似，是用来将matplotlib在日常实践中作的图片作一个总结，方便以后查询上手。
<!-- more -->


## 简介
Matlplotlib是Python的一个可视化模块。该项目是由John D. Hunter发起的，但却是受Matlab启发构建的，并且有一套完全仿照Matlab函数形式的绘图接口。它让你方便地制作线条图、饼图、柱状图以及其它专业图形。使用Matplotlib，你可以定制所做图表的任一方面。


## 散点图
散点图是我们最常见的一种图，它一样用来显示数据点在直角坐标系平面上的分布图例。在我们不清楚数据点之间的关系时，常做该图来直观显示数据的分步情况，以便做进一步分析。
* 图例如下：  
![scatter]({{site.baseurl}}/assets/images/scatter.jpg)

* 代码解析如下：

    ```py
    """
    Simple demo of a scatter plot.
    """
    # coding=utf-8
    #!/usr/bin/python

    import numpy as np
    import matplotlib.pyplot as plt

    # matplotlib支持中文
    from pylab import mpl
    mpl.rcParams['font.sans-serif'] = ['SimHei'] #指定默认字体
    mpl.rcParams['axes.unicode_minus'] = False # 解决保存图像是符号的‘-’显示为方块的问题

    # 构造数据
    N = 50
    x = np.arange(N)
    y1 = np.random.rand(N)*25
    y2 = np.random.rand(N)*25+25


    ## scatter常用参数
    # s[ize]    点的大小
    # c[olor]   点的颜色
    # marker    点的图案
    # alpha     透明度
    # label     图例说明中的标签
    plt.scatter(x, y1, s=50, c='b', marker='+', alpha=0.5，label=‘ClassA’)
    plt.scatter(x, y2, s=100, c='r', marker='.', alpha=0.5，label=‘ClassB’)
    ## X/Y轴的的极限
    xdelt = x.max() - x.min()
    plt.xlim(x.min()-0.1*xdelt,x.max()+0.1*xdelt)
    plt.ylim(0,50)
    ## 横纵坐标说明
    plt.xlabel(u'x值说明',fontsize=16)
    plt.ylabel(u'y值说明',fontsize=16,rotation='horizontal')
    ## 添加图例
    plt.legend(loc=‘upper left’，frameon=True)
    ## 图的标题
    plt.title(u'scatter图',fontsize=20)
    ## 保存图片
    plt.savefig('scatter.jpg')
    ## 显示图片
    plt.show()
    ```

## 折线图
折线图也是我们常见的一种图，它常用来显示数据的走向趋势。在数据分析中，常用来处理随时间而变化的连续数据。

* 图例如下：  
![polygonal]({{site.baseurl}}/assets/images/polygonal.jpg)

* 代码解析如下：

    ```py
    """
    Simple demo of a polygonal plot.
    """
    # coding=utf-8
    #!/usr/bin/python

    import numpy as np
    import matplotlib.pyplot as plt

    # matplotlib支持中文
    from pylab import mpl
    mpl.rcParams['font.sans-serif'] = ['SimHei'] #指定默认字体
    mpl.rcParams['axes.unicode_minus'] = False # 解决保存图像是符号的‘-’显示为方块的问题

    # 构造数据
    N = 50
    x = np.linspace(-2,2,N)
    y1 = x**3
    y2 = np.sin(x)


    ## plot常用参数
    # 'b'       设置颜色和点的图案
    # marker    点的图案
    # label     图例说明中的标签
    # linewidth 线宽
    plt.plot(x, y1, 'b*-', label=‘$x^3$’, linewidth=2)
    plt.plot(x, y2, 'r', label=‘$sin(x)$’, linewidth=2)
    ## 设置坐标轴
    ax= plt.gca()       # 获取当前坐标系实例
    # 轴线/标尺设置
    ax.spines['right'].set_visible(False)
    ax.spines['top'].set_visible(False)
    ax.xaxis.set_ticks_position('bottom')   # X轴标尺在轴线下面
    ax.spines['bottom'].set_position(('data',0))    # 底部轴线在数据区0的位置
    ax.yaxis.set_ticks_position('left')     # Y轴标尺在轴线左边
    ax.spines['left'].set_position(('data',0))  # 左边轴线在数据区0的位置
    ## X/Y轴的的极限
    xdelt = x.max() - x.min()
    plt.xlim(x.min()-0.1*xdelt,x.max()+0.1*xdelt)
    plt.ylim(0,50)
    ## 横纵坐标说明
    plt.xlabel(u'x值说明',fontsize=16)
    plt.ylabel(u'y值说明',fontsize=16,rotation='horizontal')
    ## 添加图例
    plt.legend(loc=‘upper left’，frameon=True)
    ## 图的标题
    plt.title(u'折线图',fontsize=20)
    ## 保存图片
    plt.savefig('polygonal.jpg')
    ## 显示图片
    plt.show()
    ```

## 柱状图
柱状图也是我们常见的一种图，它也叫条图，是一种以长方形的长度为变量的表达图形的统计报告图，由一系列高度不等的纵向条纹表示数据分布的情况，用来比较两个或以上的价值。在数据分析中，常用来比较不同的模型而产生的不同结果。

* 图例如下：  
![histogram]({{site.baseurl}}/assets/images/histogram.jpg)

* 代码解析如下：

    ```py
    """
    Simple demo of a histogram plot.
    """
    # coding=utf-8
    #!/usr/bin/python

    import numpy as np
    import matplotlib.pyplot as plt

    # matplotlib支持中文
    from pylab import mpl
    mpl.rcParams['font.sans-serif'] = ['SimHei'] #指定默认字体
    mpl.rcParams['axes.unicode_minus'] = False # 解决保存图像是符号的‘-’显示为方块的问题

    # 构造数据
    mu = 100
    sigma = 15
    x = mu + sigma * np.random.randn(10000)


    num_bins = 5
    ## hist常用参数
    # num_bins  条数
    # marker    点的图案
    # label     图例说明中的标签
    # linewidth 线宽
    plt.ot(x, y1, 'b', label=‘$x^3$’, linewidth=2)
    plt.plot(x, y2, 'r', label=‘$sin(x)$’, linewidth=2)
    ## 设置坐标轴
    ax= plt.gca()       # 获取当前坐标系实例
    # 轴线/标尺设置
    ax.spines['right'].set_visible(False)
    ax.spines['top'].set_visible(False)
    ax.xaxis.set_ticks_position('bottom')   # X轴标尺在轴线下面
    ax.spines['bottom'].set_position(('data',0))    # 底部轴线在数据区0的位置
    ax.yaxis.set_ticks_position('left')     # Y轴标尺在轴线左边
    ax.spines['left'].set_position(('data',0))  # 左边轴线在数据区0的位置
    ## X/Y轴的的极限
    xdelt = x.max() - x.min()
    plt.xlim(x.min()-0.1*xdelt,x.max()+0.1*xdelt)
    plt.ylim(0,50)
    ## 横纵坐标说明
    plt.xlabel(u'x值说明',fontsize=16)
    plt.ylabel(u'y值说明',fontsize=16,rotation='horizontal')
    ## 添加图例
    plt.legend(loc=‘upper left’，frameon=True)
    ## 图的标题
    plt.title(u'折线图',fontsize=20)
    ## 保存图片
    plt.savefig('polygonal.jpg')
    ## 显示图片
    plt.show()
    ```

## section



## 参考文献
1. [matplotlib官网图例][plt_org]
2. [matplotlib源码][plt_git]
3. [matplotlib入门][plt_tour]


[plt_org]: http://matplotlib.org
[plt_git]:  https://github.com/matplotlib
[plt_tour]: http://reverland.org/python/2012/09/07/matplotlib-tutorial/
