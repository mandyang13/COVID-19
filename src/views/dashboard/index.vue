<template>
  <div class="dashboard-container">
    <div class="dashboard-text">Status of COVID-19 cases in Ontario</div>
    <apexchart
      width="100%"
      type="line"
      :options="chartOptions"
      :series="series"
      style="margin:20px 0;"
    />
    <div style="margin-bottom: 40px; color: gray;">
      Please see COVID-19 pandemic in Ontario main events logs
      <a href="https://en.wikipedia.org/wiki/COVID-19_pandemic_in_Ontario" target="_blank">here</a>
    </div>
    <apexchart type="bar" height="350" :options="barOptions" :series="barSeries" />
    <apexchart
      width="100%"
      type="line"
      :options="mutOptions"
      :series="mutSeries"
      style="margin:20px 0;"
    />
  </div>
</template>

<script>
import Covid from './cov.json'
import moment from 'moment'
export default {
  data() {
    return {
      cov: Covid,
      series: [
        {
          name: 'Confirmed Positive',
          data: []
        }
      ],
      chartOptions: {
        xaxis: {
          categories: [],
          type: 'datetime'
        },
        chart: {
          id: 'COVID-19 Ontario',
          type: 'area',
          stacked: false,
          height: 350,
          zoom: {
            type: 'x',
            enabled: true,
            autoScaleYaxis: true
          },
          toolbar: {
            autoSelected: 'zoom'
          }
        },
        dataLabels: {
          enabled: false
        },
        tooltip: {
          x: {
            format: 'dd MMM yyyy'
          }
        },
        title: {
          text: 'Total confirmed positive in Ontario',
          align: 'left'
        },
        annotations: {
          xaxis: [{
            x: new Date('15 Apr 2020').getTime(),
            strokeDashArray: 0,
            borderColor: '#ff0000',
            label: {
              borderColor: '#ff0000',
              offsetY: '100px',
              style: {
                color: '#fff',
                background: '#ff0000'
              },
              text: 'stay-at-home order'
            }
          }, {
            x: new Date('12 Aug 2020').getTime(),
            strokeDashArray: 0,
            borderColor: '#08f13c',
            label: {
              borderColor: '#08f13c',
              offsetY: '100px',
              style: {
                color: '#fff',
                background: '#08f13c'
              },
              text: 'restrictions lifted (Stage 3)'
            }
          }, {
            x: new Date('14 Jan 2021').getTime(),
            x2: new Date('8 Mar 2021').getTime(),
            fillColor: '#ff000094',
            opacity: 0.4,
            label: {
              borderColor: '#ff0000',
              style: {
                fontSize: '10px',
                color: '#fff',
                background: '#ff0000'
              },
              offsetY: -6,
              text: 'stay-at-home order'
            }
          }, {
            x: new Date('3 Apr 2021').getTime(),
            strokeDashArray: 0,
            borderColor: '#ff0000',
            label: {
              borderColor: '#ff0000',
              offsetY: '100px',
              style: {
                color: '#fff',
                background: '#ff0000'
              },
              text: 'stay-at-home order'
            }
          }],
          points: [{
            x: new Date('14 Dec 2020').getTime(),
            y: 16586,
            marker: {
              size: 8,
              fillColor: '#fff',
              strokeColor: '#a52a2a',
              radius: 2,
              cssClass: 'apexcharts-custom-class'
            },
            label: {
              borderColor: '#a52a2a',
              offsetY: 0,
              style: {
                color: '#fff',
                background: '#a52a2a'
              },

              text: 'Vaccine'
            }
          }]
        }
      },
      barSeries: [{
        name: 'Confirmed Positive',
        type: 'line',
        data: []
      }, {
        name: 'Hospitalized',
        type: 'column',
        data: []
      }, {
        name: 'in ICU',
        type: 'column',
        data: []
      }, {
        name: 'on Ventilator',
        type: 'column',
        data: []
      }],
      barOptions: {
        chart: {
          height: 350,
          type: 'line',
          stacked: false
        },
        plotOptions: {
          bar: {
            // horizontal: false,
            columnWidth: '55%'
            // endingShape: 'rounded'
          }
        },
        colors: ['#f5b145', '#99C2A2', '#C5EDAC', '#66C7F4'],
        stroke: {
          width: 2
        },
        xaxis: {
          categories: ['2020-Q2', '2020-Q3', '2020-Q4', '2021-Q1']
        },
        yaxis: [
          {
            seriesName: 'Confirmed Positive',
            axisTicks: {
              show: true
            },
            axisBorder: {
              show: true
            },
            title: {
              text: 'Number of Cases'
            }
          },
          {
            seriesName: 'Hospitalized',
            opposite: true,
            axisTicks: {
              show: true
            },
            axisBorder: {
              show: true
            },
            title: {
              text: 'Number of Cases'
            }
          }, {
            seriesName: 'Hospitalized',
            show: false
          }, {
            seriesName: 'Hospitalized',
            show: false
          }
        ],
        // fill: {
        //   opacity: 1
        // },
        dataLabels: {
          enabled: true,
          enabledOnSeries: [0],
          style: {
            fontSize: '0px'
          }
        },
        markers: {
          size: 8
        },
        legend: {
          horizontalAlign: 'left',
          offsetX: 40
        }
      },
      mutSeries: [{
        name: 'Lineage B.1.1.7',
        data: [10, 41, 35, 51, 49, 62, 69, 91, 148]
      },
      {
        name: 'Lineage B.1.351',
        data: [11, 41, 35, 51, 49, 62, 69, 91, 148]
      },
      {
        name: 'Lineage P.1',
        data: [12, 41, 35, 51, 49, 62, 69, 91, 148]
      }],
      mutOptions: {
        colors: ['#99C2A2', '#C5EDAC', '#66C7F4'],
        chart: {
          height: 350,
          type: 'line',
          zoom: {
            enabled: false
          }
        },
        dataLabels: {
          enabled: false
        },
        tooltip: {
          x: {
            format: 'dd MMM yyyy'
          }
        },
        title: {
          text: 'Total confirmed positive in Ontario (new lineages)',
          align: 'left'
        },
        xaxis: {
          categories: [],
          type: 'datetime'
        }
      }
    }
  },
  mounted() {
    this.postiveLine()
    this.postiveBar()
    this.mutationLine()
    // console.log(this.cov, 111)
  },
  methods: {
    postiveLine() {
      var dateList = []
      var resultList = []
      for (var item of this.cov) {
        for (var i in item) {
          if (i === 'Reported Date') {
            dateList.push(item[i])
          } else if (i === 'Confirmed Positive') {
            resultList.push(item[i] === '' ? 0 : parseInt(item[i]))
          }
        }
        // if (item['Reported Date'] === '02/06/2020') {
        //   break
        // }
      }
      this.series = [{
        data: resultList
      }]
      this.chartOptions = {
        xaxis: {
          categories: dateList
        }
      }
    },
    postiveBar() {
      var cat1 = []
      var cat2 = []
      var cat3 = []
      var cat4 = []
      var flag = false
      var d = new Date('05/01/2020')
      for (var item of this.cov) {
        for (var i in item) {
          if (i === 'Reported Date') {
            if (this.moment(item[i], 'DD/MM/YYYY').toDate() > d) {
              flag = true
            }
          }
          if (flag && i === 'Confirmed Positive') {
            cat1.push(item[i] === '' ? 0 : parseInt(item[i]))
          } else if (flag && i === 'Number of patients hospitalized with COVID-19') {
            cat2.push(item[i] === '' ? 0 : parseInt(item[i]))
          } else if (flag && i === 'Number of patients in ICU due to COVID-19') {
            cat3.push(item[i] === '' ? 0 : parseInt(item[i]))
          } else if (flag && i === 'Number of patients in ICU on a ventilator due to COVID-19') {
            cat4.push(item[i] === '' ? 0 : parseInt(item[i]))
          }
        }
        // if (item['Reported Date'] === '02/06/2020') {
        //   break
        // }
      }
      var q = cat1.length / 4
      var cat1q = this.avgEvery(cat1, q)
      var cat2q = this.avgEvery(cat2, q)
      var cat3q = this.avgEvery(cat3, q)
      var cat4q = this.avgEvery(cat4, q)
      // console.log(cat1q, cat2q, cat3q, cat4q, 22222)
      this.barSeries = [{
        data: cat1q
      }, {
        data: cat2q
      }, {
        data: cat3q
      }, {
        data: cat4q
      }]
    },
    avgEvery(arr, n) {
      var result = []
      for (var i = 0; i < arr.length;) {
        var sum = 0
        for (var j = 0; j < n; j++) {
          sum += +arr[i++] || 0
        }
        result.push(Math.floor(sum / n))
      }
      return result
    },
    mutationLine() {
      var dateList = []
      var mut1 = []
      var mut2 = []
      var mut3 = []
      var flag = false
      var d = new Date('01/28/2021')
      for (var item of this.cov) {
        for (var i in item) {
          if (i === 'Reported Date') {
            if (this.moment(item[i], 'DD/MM/YYYY').toDate() > d) {
              flag = true
              dateList.push(item[i])
            }
          } else if (flag && i === 'Total_Lineage_B-1-1-7') {
            mut1.push(item[i] === '' ? 0 : parseInt(item[i]))
          } else if (flag && i === 'Total_Lineage_B-1-351') {
            mut2.push(item[i] === '' ? 0 : parseInt(item[i]))
          } else if (flag && i === 'Total_Lineage_P-1') {
            mut3.push(item[i] === '' ? 0 : parseInt(item[i]))
          }
        }
      }
      // console.log(dateList, mut1, mut2, mut3, 111)
      this.mutSeries = [{
        data: mut1
      }, {
        data: mut2
      }, {
        data: mut3
      }]
      this.mutOptions = {
        xaxis: {
          categories: dateList
        }
      }
    },
    moment(date) {
      return moment(date)
    }
  }
}
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
.chart-container {
  position: relative;
  width: 100%;
  height: calc(100vh - 84px);
}
a:link, a:visited {
  color: blue;
  text-decoration: underline;
  cursor: pointer;
}
</style>
