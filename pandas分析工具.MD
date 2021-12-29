# 一个神奇的库pandas-profiling

最近发现一个神奇的库pandas-profiling，**一行代码**生成**超详细数据分析报告**，实乃我等数据分析从业者的福音哈哈~ 



一键生成超详细数据分析报告

一般来说，面对一个数据集，我们需要做一些探索性分析 (Exploratory data analysis)，这个过程繁琐而冗杂。以泰坦尼克号数据集为例，传统方法是先用Dataframe.describe()：

```text
import pandas as pd

data = pd.read_csv('https://raw.githubusercontent.com/datasciencedojo/datasets/master/titanic.csv')
data.describe()
```

![img](https://pic1.zhimg.com/50/v2-8768711ba6b36ff23353dfe0aa58df27_720w.jpg?source=1940ef5c)![img](https://pic1.zhimg.com/80/v2-8768711ba6b36ff23353dfe0aa58df27_720w.jpg?source=1940ef5c)

通过describe()方法，我们对数据集可以有一个大体的认知。然后，通过分析各变量之间的关系（直方图，散点图，柱状图，关联分析等等），我们可以进一步探索这个数据集。EDA这个步骤通常需要耗费大量的时间和精力。如今，有了pandas-profiling库，我们一行代码就可以生成一份超详细的数据分析报告~



```text
import pandas_profiling  

data.profile_report(title='Titanic Dataset')
```

具体报告效果如下：

![img](https://pic2.zhimg.com/80/v2-faf97e710da736d8f1d3785efbf7d678_720w.jpg?source=1940ef5c)