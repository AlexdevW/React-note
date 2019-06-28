# 工具

1. **Moment.js**  JavaScript 日期处理类库

   #### 日期格式化

```js
moment().format('MMMM Do YYYY, h:mm:ss a'); // 六月 28日 2019, 8:28:34 晚上
moment().format('dddd');                    // 星期五
moment().format("MMM Do YY");               // 6月 28日 19
moment().format('YYYY [escaped] YYYY');     // 2019 escaped 2019
moment().format();                          // 2019-06-28T20:28:34+08:00
```

2. **XLSX** 导出excel 文件

```js
exportFile = () => {
    /* convert state to workbook */
    const ws = XLSX.utils.aoa_to_sheet(this.state.data); // 文件内容
    const wb = XLSX.utils.book_new();
    XLSX.utils.book_append_sheet(wb, ws, "SheetJS");
    /* generate XLSX file and send to client */
    XLSX.writeFile(wb, "sheetjs.xlsx")
}
```

3. **wangEditor** 富文本框编辑器 

```js
constructor () {
    super()
    this.editorRef = createRef()
    this.editor = null
}

initEditor = () => {
    // 创建 wangeditor 对象实例
    this.editor = new E(this.editorRef.current)
    // 添加配置
    this.editor.customConfig.onchange = html =>　{
        this.props.form.setFieldsValue({
            content: html
        })
    }
    // 创建
    this.editor.create()
}
```

4. echarts  百度图表 可视化图表          Antv

```js
  constructor() {
    super()
    this.articleChartRef = createRef()
    this.articleChart = null
  }

  initChart = () => {
    // 初始化 echarts
    this.articleChart = echarts.init(this.articleChartRef.current)
    // 设置 option
    const option = {
      xAxis: {
        type: 'category',
        boundaryGap: false,
        data: amount.map(item => item.month) // amount const定义amount数据 [{a:123,b:3},{}]
      },
      yAxis: {
        type: 'value',
      },
      series: [{
        data: amount.map(item => item.value),
        type: 'line',
        areaStyle: {}
      }]
    }
    this.articleChart.setOption(option)
  }

  componentDidMount() {
    this.initChart()
  }
```

