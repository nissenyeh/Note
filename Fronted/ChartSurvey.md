### 前端報表library研究


| library | 社群支援  |圖表|風格| 是否支援Vue |
| -------- | -------- | -------- |-------- |-------- |
| [ApexCharts JS](https://apexcharts.com/vue-chart-demos/)| [6.1K Star](https://github.com/apexcharts)  | SVG繪圖＋輕量級＋伸縮方便| 簡約風格[(Demo)](https://apexcharts.com/vue-chart-demos/) | [是](https://github.com/apexcharts/vue-apexcharts)|
|[ECharts](https://echarts.baidu.com/)|[33K Star](https://github.com/apache/incubator-echarts)|CANVAS+支援複雜圖表| 學術風格[(Demo)](https://echarts.baidu.com/examples/)|[1.是](https://github.com/ecomfe/vue-echarts)<Br>[2.饿了么前端4.3K](https://v-charts.js.org/)
|[Hichart](https://www.highcharts.com/)|[8.6K Star](https://github.com/highcharts/highcharts)|CANVAS+支援複雜圖表| 學術風格[(Demo)](https://www.highcharts.com/demo)|[是](https://github.com/highcharts/highcharts-vue)
|[ChartJS](https://www.chartjs.org/)|[43K Star](https://github.com/chartjs/Chart.js)|CANVAS+輕量級+伸縮要用插件| 簡約風格[(Demo)](https://www.chartjs.org/samples/latest/)|1.原團隊沒有<Br>2.[個人製作Apertureless(2.9K)](https://github.com/apertureless/vue-chartjs)


- 以上至少都可以製作折線圖、柱狀圖、圓餅圖、雷達圖、分佈圖、泡泡圖.....等

### 圖表比較


#### ApexChart

- SVG繪圖
- 相對於ApexChart，ApexChart更好的縮放/平移、註釋功能

#### ChartJS

- Canvas繪圖
- 相對於Hichart，大部分人喜歡ChartJS，因為該庫包含一組6個圖表，並且是11Kb gzip壓縮，這使得它的加載時間和頁面影響很小。（min版總大小50多k）
- 缺點是沒有很好縮放/平移、註釋功能的功能

#### Hichart

- 文檔清楚，一個公司負責的項目
- 當你發現你有大量的交互是通過外部的按鈕來觸發chart內部的變化的時候, highchart就是你最好的選擇


