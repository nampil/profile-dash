<template>
  <div class="statistics">
    <div class="stats">
      <h2>Statistics</h2>
      <div class="stats_group">
        <div class="stats_item">
          <h3>Total views</h3>
          <p>72.593</p>
        </div>
        <div class="stats_item">
          <h3>This week</h3>
          <p>9.307</p>
        </div>
        <div class="stats_item">
          <h3>Today</h3>
          <p>1.328</p>
        </div>
      </div>
    </div>
    <div class="graph">
      <line-chart ref="lineChartRef" v-bind="lineChartProps"></line-chart>
    </div>
  </div>
</template>

<script setup>
  import { onMounted, ref, computed } from 'vue'
  import { LineChart, useLineChart } from 'vue-chart-3'
  import { Chart, registerables } from 'chart.js'
  import ChartDataLabels from 'chartjs-plugin-datalabels'

  Chart.register(...registerables, ChartDataLabels)

  const timeSpend = ref([15, 12, 25, 18, 16, 20])

  const ctx = ref(null)
  const gradientOne = ref(null)
  const gradientTwo = ref(null)
  const effectOnLastPoint = (pointRadiusBase, length, dataArray) => {
    const result = dataArray || [pointRadiusBase]
    while (result.length < length) {
      result.unshift(0)
    }
    return result
  }

  const chartData = computed(() => {
    return {
      labels: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
      datasets: [
        {
          label: 'Time Spend',
          data: timeSpend.value,
          borderWidth: 3,
          tension: 0.4,
          pointRadius: effectOnLastPoint(4, timeSpend.value.length),
          borderColor: 'rgba(123, 139, 249, 1)',
          datalabels: {
            labels: {
              title: {},
              dot: {
                backgroundColor: '#F5E306',
                offset: 15,
                formatter: () => '',
                rotation: 45,
                borderRadius: 0,
                padding: { top: 0, bottom: 0, left: 7, right: 7 },
              },
            },
            display: (context) =>
              context.dataIndex === timeSpend.value.length - 1 ? true : false,
            align: 'top',
            anchor: 'start',
            offset: 20,
            formatter: (value, context) => value + ' min',
            backgroundColor: '#F5E306',
            borderRadius: 6,
            padding: { top: 4, bottom: 4, left: 14, right: 14 },
          },
        },
        {
          label: '',
          data: [12, 10, 15, 20, 22, 13, 25],
          borderWidth: 1,
          backgroundColor: () => gradientTwo.value,
          fill: true,
          tension: 0.4,
          pointRadius: 0,
          datalabels: {
            display: false,
          },
        },
      ],
    }
  })

  const chartOptions = computed(() => ({
    responsive: true,
    scales: {
      y: {
        display: false,
        beginAtZero: true,
      },
      x: {
        ticks: {
          color: '#768BC4',
          font: (context) => {
            const fontConfig = {
              family: "'proxima-nova', san-serif",
              size: 12,
              weight: 'normal',
            }
            if (context.index === timeSpend.value.length - 1) {
              fontConfig.weight = 'bold'
              fontConfig.size = '14'
            }
            return fontConfig
          },
        },

        grid: {
          display: false,
          borderWidth: 0,
        },
      },
    },
    plugins: {
      legend: {
        align: 'start',
        position: 'top',
        labels: {
          boxWidth: 0,
          color: '#252E48',
          font: {
            weight: 'bold',
          },
        },
      },
      datalabels: {
        font: {
          family: "'proxima-nova', san-serif",
          size: 12,
        },
      },
    },
  }))
  const { lineChartProps, lineChartRef } = useLineChart({
    chartData,
    options: chartOptions,
    height: '100%',
    width: '100%',
  })

  onMounted(() => {
    ctx.value = lineChartRef.value.chartInstance.ctx

    gradientOne.value = ctx.value.createLinearGradient(
      0,
      0,
      0,
      ctx.value.canvas.height
    )

    gradientOne.value.addColorStop(0, 'rgba(197, 206, 239, 0.3)')
    gradientOne.value.addColorStop(0.8, 'rgba(255, 255, 255, 1)')

    gradientTwo.value = ctx.value.createRadialGradient(
      ctx.value.canvas.width / 2,
      0,
      20,
      ctx.value.canvas.width / 2,
      0,
      ctx.value.canvas.height
    )
    gradientTwo.value.addColorStop(0.96, 'rgba(255, 255, 255, 1)')
    gradientTwo.value.addColorStop(0, 'rgba(197, 206, 239, 0.3)')

    lineChartRef.value.update()
  })
</script>

<style lang="scss" scoped></style>
