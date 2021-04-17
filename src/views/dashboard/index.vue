<template>
  <div class="dashboard-container">
    <div class="dashboard-text">Status of COVID-19 cases in Ontario</div>
    <apexchart
      width="500"
      type="bar"
      :options="chartOptions"
      :series="series"
    ></apexchart>
  </div>
</template>

<script>
export default {
  data() {
    return {
      chartOptions: {
        chart: {
          id: 'vuechart-example'
        },
        xaxis: {
          categories: [1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998]
        }
      },
      series: [
        {
          name: 'series-1',
          data: [30, 40, 35, 50, 49, 60, 70, 91]
        }
      ]
    }
  },
  mounted() {
    // var data = JSON.parse('@/cov.json')
    // console.log(data, 111)
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
</style>
