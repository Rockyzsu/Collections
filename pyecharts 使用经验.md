# pyecharts 使用经验



## 全局配置

set_global_opts() [注意,不是在**初始化**里面]

里面设置标题:

title_opts=opts.TitleOpts(title="主标题", subtitle="副标题")

TitleOpts -> title_opts



```python
scatter = (
    Scatter(init_opts=opts.InitOpts(width="1024px", height="768px",bg_color=JsCode(background_color_js)))
    .add_xaxis(xaxis_data=X)
    .add_yaxis(
        series_name="上市价格",
        y_axis=Y,
        symbol_size=10,
        label_opts=opts.LabelOpts(is_show=False),
    )
    .set_series_opts()
    .set_global_opts(
        title_opts=opts.TitleOpts(title='转债上市价格预测'),
        xaxis_opts=opts.AxisOpts(
            type_="value", 
            splitline_opts=opts.SplitLineOpts(is_show=True),
            min_=60,
        ),
        yaxis_opts=opts.AxisOpts(
            name='我是y轴,右边的', # 坐标轴的显示名字
            type_="value",
            axistick_opts=opts.AxisTickOpts(is_show=True),
            splitline_opts=opts.SplitLineOpts(is_show=True),
            min_=60,
            
        ),
        tooltip_opts=opts.TooltipOpts(is_show=False),
    )
)
scatter.render('only.html')
```





## 多图绘制

```python
scatter = (
    Scatter(init_opts=opts.InitOpts(width="800px", height="600px"))
    .add_xaxis(xaxis_data=X)
    .add_yaxis(
        series_name="转债价格",
        y_axis=Y,
        symbol_size=3,
        label_opts=opts.LabelOpts(is_show=False),
    )
    .set_series_opts()
    .set_global_opts(
        xaxis_opts=opts.AxisOpts(
            type_="value", splitline_opts=opts.SplitLineOpts(is_show=True),
            min_=60,
        ),
        yaxis_opts=opts.AxisOpts(
            type_="value",
            axistick_opts=opts.AxisTickOpts(is_show=True),
            splitline_opts=opts.SplitLineOpts(is_show=True),
            min_=60,
            
        )
    )
)

line = (
    Line()
    .add_xaxis(xaxis_data=X0)
    .add_yaxis(
        series_name="可转债价格预测",
        # yaxis_index=1,
        symbol_size=5,
        y_axis=Y0,
        label_opts=opts.LabelOpts(is_show=False),
        linestyle_opts=opts.LineStyleOpts(width=1,color='yellow'),
        
    ).set_colors("yellow") 
)
scatter.overlap(line)
scatter.render_notebook()
```

* 如果需要2条Y轴,需要 设置 yaxis_index=1.