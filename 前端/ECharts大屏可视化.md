# ECharts

[toc]

> 技术栈

* 基于flexible.js + rem 智能大屏适配
* VScode cssrem插件
* Flex 布局
* Less使用
* 基于ECharts数据可视化展示
* ECharts 柱状图数据设置
* ECharts 地图引入ا

## vue加ECharts

1. 下安装echarts载包`npm install echarts --save-dev`

2. 引入main.js当中

   ```js
   import * as echarts from 'echarts'
   Vue.prototype.$echarts = echarts
   ```

   