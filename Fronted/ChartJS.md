
### ChartJS


- [ChartJS](https://www.chartjs.org/)本身是以canvas為基礎的libiary
- [中文文檔](https://chartjs-doc.abingoal.com/)


#### 如何調整ChartJS大小？

- Canvas本身不能調整長寬，而是根據父層自適應。所以要調整外層長寬（這裡是 .myChart)
- 如果圖表想要有橫向捲軸的功能，可以於外層再包div，然後設定overflow-x: scroll;（這裡是 .chartWrapper)


```
    <div class="chartWrapper">
      <div class="myChart">
        <canvas id="myChart"></canvas>
      </div>
    </div>
```

```
.chartWrapper {
  width:100%;
  overflow-x: scroll;
}

.myChart {
  width:8000px;
  height:450px;
}
```

- ChartJS本身是以canvas為基礎的libiary
- Canvas本身不能調整長寬，而是根據父層自適應。所以要調整外層長寬（這裡是 .myChart)
- 如果圖表想要有橫向捲軸的功能，可以於外層再包div，然後設定overflow-x: scroll;（這裡是 .chartWrapper)

### 如何把資料丟到ChartJS裡面？

- 把資料放在`data`裡面


```
var myChart
function render() {
  var canvas = document.getElementById('myChart').getContext('2d');
  myChart = new Chart(canvas, {
              type: 'bar',
              data: {
                labels: departmentNameList,
                datasets: [{
                  label: '科室人數',
                  data: numberOfdepartments,
                }]
              },
              options: {
                plugins:{
                  labels:{
                    render:'value',
                  },
                },
                layout:{
                  padding: {          
                    top: 30
                  }
                },
                legend: {
                  position: 'left'
                },
                maintainAspectRatio: false,
                scales: {
                  xAxes: [{
                    categorySpacing: 10,
                  }]
                }
              },
              });
  }
render()
```

#### 如何更新ChartJS圖表？

- 利用update()可以更新圖表，這樣避免重複繪圖

```
function ChartUpdata(newYaxisData,labelName) {
  var Data = [{
    label:labelName,
    data: newYaxisData
  }]
  myChart.config.data.datasets = Data
  myChart.update();
}
```

#### 如何設定ChartJS的padding？

- 在`option`的`layout`的padding裡面設定

```
  myChart = new Chart(canvas, {
              type: 'bar',
              data: {
                labels: departmentNameList,
                datasets: [{
                  label: '科室人數',
                  data: numberOfdepartments,
                }]
              },
              options: {
                plugins:{
                  labels:{
                    render:'value',
                  },
                },
                layout:{
                  padding: {          
                    top: 30
                  }
                },
                legend: {
                  position: 'left'
                },
                maintainAspectRatio: false,
                scales: {
                  xAxes: [{
                    categorySpacing: 10,
                  }]
                }
              },
              });
  }
render()
```

#### Plugin

- [chartjs-plugin-labels](https://github.com/emn178/chartjs-plugin-labels)：可以用來顯示圖表的數字

