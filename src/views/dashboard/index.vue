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
    <div>Please see COVID-19 pandemic in Ontario main events logs <a href="https://en.wikipedia.org/wiki/COVID-19_pandemic_in_Ontario" target="_blank">here</a></div>
  </div>
</template>

<script>
import Covid from './cov.json'
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
      }
    }
  },
  mounted() {
    this.postiveLine()
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
