# wx-charts
微信小程序图表工具，charts for WeChat small app

基于canvas绘制，体积小巧

**持续优化更新中，请保持关注~ 有任何问题欢迎在[Issues](https://github.com/xiaolin3303/wx-charts/issues)中讨论**

**支持图表类型**
- 饼图   `pie`
- 圆环图 `ring`
- 线图   `line`
- 柱状图 `column`
- 区域图 `area`

代码分析 [Here](https://segmentfault.com/a/1190000007649376)

# 更新记录 

- [ ] 动画性能优化
- [x] add animation  2016-12-05
- [x] build with `rollup` 2016-12-02
- [x] add legend  2016-11-29

# 如何使用
1、直接引用编译好的文件 `dist/charts.js`

2、自行编译

```
git clone https://github.com/xiaolin3303/wx-charts.git
npm install rollup -g
npm install
rollup -c 或者 rollup --config rollup.config.prod.js
```

# 参数说明
`opts` Object

`opts.canvasId` String **required** 微信小程序canvas-id

`opts.width` Number **required** canvas宽度，单位为px

`opts.height` Number **required** canvas高度，单位为px

`opts.animation` Boolean default `true` 是否动画展示

`opts.type` String **required** 图表类型，可选值为`pie`, `line`, `column`, `area`, `ring`

`opts.categories` Array **required** *(饼图不需要)* 数据类别分类

`opts.dataLabel` Boolean default `true` 是否在图表中显示数据内容值

`opts.yAxis` Object Y轴配置

`opts.yAxis.format` Function 自定义Y轴文案显示

`opts.yAxis.min` Number Y轴起始值

`opts.yAxis.title` String Y轴title

`opts.series` Array **required** 数据列表

**数据列表每项结构定义**

`dataItem` Object

`dataItem.data` Array **required** *(饼图为Number)* 数据

`dataItem.color` String 例如`#7cb5ec` 不传入则使用系统默认配色方案

`dataItem.name` String 数据名称

`dateItem.format` Function 自定义显示数据内容

# Example

### pie chart

```javascript
var Charts = require('charts.js');
new Charts({
    canvasId: 'pieCanvas',
    type: 'pie',
    series: [{
        name: '成交量1',
        data: 15,
    }, {
        name: '成交量2',
        data: 35,
    }, {
        name: '成交量3',
        data: 78,
    }, {
        name: '成交量4',
        data: 63,
    }],
    width: 320,
    height: 200,
    dataLabel: false
});
```
![pieChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/pie.png)
![pieChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/pie.gif)

### ring chart

```javascript
new Charts({
    canvasId: 'pieCanvas',
    type: 'ring',
    series: [{
        name: '成交量1',
        data: 15,
    }, {
        name: '成交量2',
        data: 35,
    }, {
        name: '成交量3',
        data: 78,
    }, {
        name: '成交量4',
        data: 63,
    }],
    width: 320,
    height: 200,
    dataLabel: false
});
```
![pieChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/ring.png)
![pieChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/ring.gif)

### line chart

```javascript
new Charts({
    canvasId: 'lineCanvas',
    type: 'line',
    categories: ['2012', '2013', '2014', '2015', '2016', '2017'],
    series: [{
        name: '成交量1',
        data: [0.15, 0.2, 0.45, 0.37, 0.4, 0.8],
        format: function (val) {
            return val.toFixed(2) + '万';
        }
    }, {
        name: '成交量2',
        data: [0.30, 0.37, 0.65, 0.78, 0.69, 0.94],
        format: function (val) {
            return val.toFixed(2) + '万';
        }
    }],
    yAxis: {
        title: '成交金额 (万元)',
        format: function (val) {
            return val.toFixed(2);
        },
        min: 0
    },
    width: 320,
    height: 200
});
```

![lineChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/line.png)
![lineChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/line.gif)

### columnChart

```javascript
new Charts({
    canvasId: 'columnCanvas',
    type: 'column',
    categories: ['2012', '2013', '2014', '2015', '2016', '2017'],
    series: [{
        name: '成交量1',
        data: [15, 20, 45, 37, 4, 80]
    }, {
        name: '成交量2',
        data: [70, 40, 65, 100, 34, 18]
    }],
    yAxis: {
        format: function (val) {
            return val + '万';
        }
    },
    width: 320,
    height: 200
});
```

![columnChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/column.png)
![columnChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/column.gif)

### areaChart

```javascript
new Charts({
    canvasId: 'areaCanvas',
    type: 'area',
    categories: ['2016-08', '2016-09', '2016-10', '2016-11', '2016-12', '2017'],
    series: [{
        name: '成交量1',
        data: [70, 40, 65, 100, 34, 18],
        format: function (val) {
            return val.toFixed(2) + '万';
        }
    }, {
        name: '成交量2',
        data: [15, 20, 45, 37, 4, 80],
        format: function (val) {
            return val.toFixed(2) + '万';
        }
    }],
    yAxis: {
        format: function (val) {
            return val + '万';
        }
    },
    width: 320,
    height: 200
});
```

![areaChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/area.png)
![areaChart](https://raw.githubusercontent.com/xiaolin3303/wx-charts/master/example/area.gif)

# 测试 
1. iPhone 6s, IOS 9.3.5
2. 小米4, ANDORID 6.0.1

兼容性问题请在[Issue](https://github.com/xiaolin3303/wx-charts/issues)中提出
