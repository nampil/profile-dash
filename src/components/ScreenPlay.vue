<template>
  <div class="screenplay">
    <div class="stats">
      <h2>Screen Play</h2>
      <div class="stats_group">
        <div class="stats_item">
          <h3>Recorded</h3>
          <p>133 <span>min</span></p>
        </div>
        <div class="stats_item">
          <h3>Today</h3>
          <p>12 <span>min</span></p>
        </div>
      </div>
    </div>
    <div class="graph">
      <div
        class="goal-progress"
        :style="`--circle-progress: ${progress}; --circle-strokeDasharray: ${strokeDasharray}; --circumference: ${circumference};`"
      >
        <h3>Goal Progress</h3>

        <svg viewBox="0 0 100 100">
          <circle
            ref="base-circle"
            class="base-circle"
            stroke-width="8%"
            fill="none"
            stroke="#333"
            cx="50%"
            cy="50%"
            r="45%"
          />
          <circle
            ref="statCircle"
            class="stat-circle"
            stroke-width="8%"
            cx="50%"
            cy="50%"
            r="45%"
          />
          <text x="50%" y="50%" dy="0.4em" text-anchor="middle">
            {{ percent }}%
          </text>
        </svg>
      </div>
      <div class="daily-record">
        <h3>Daily Record</h3>
        <bar-chart v-bind="barChartProps" />
      </div>
    </div>
  </div>
</template>

<script setup>
  import { computed, onMounted, ref } from 'vue'
  import { BarChart, useBarChart } from 'vue-chart-3'
  import { Chart, registerables } from 'chart.js'
  Chart.register(...registerables)

  const initialProgress = 57.3
  const t = 3000

  const statCircle = ref(null)
  let percent = ref(0)
  const strokeDasharray = ref(null)
  const circumference = ref(null)
  const progress = computed(() => {
    return circumference.value - (percent.value / 100) * circumference.value
  })

  const updateProgress = () => {
    percent.value = parseFloat((percent.value + 1).toFixed(2))
    if (percent.value <= initialProgress) {
      requestAnimationFrame(updateProgress)
    }
  }

  // Bar Chat

  const ctx = ref(null)
  const gradientOne = ref(null)
  const gradientTwo = ref(null)
  const labels = ['29', '30', '01', '02']
  const datasetOne = {
    data: ['18', '15', '3', '12'],

    borderRadius: 5,
    datalabels: {
      labels: {
        title: {},
        dot: {
          backgroundColor: '#F5E306',
          offset: 5,
          formatter: () => '',
          rotation: 45,
          borderRadius: 0,
          padding: { top: 0, bottom: 0, left: 7, right: 7 },
        },
      },
      display: (context) =>
        context.dataIndex === datasetOne.data.length - 1 ? true : false,
      align: 'top',
      anchor: 'end',
      offset: 10,
      formatter: (value, context) => value + ' min',
      backgroundColor: '#F5E306',
      borderRadius: 6,
      padding: { top: 4, bottom: 4, left: 14, right: 14 },
    },
    backgroundColor: () => gradientOne.value,
  }
  const datasetTwo = {
    data: ['9', '13', '5', '8'],
    borderRadius: 5,

    datalabels: {
      display: false,
    },
    backgroundColor: () => gradientTwo.value,
  }

  const chartData = computed(() => {
    return {
      labels,
      datasets: [datasetOne, datasetTwo],
    }
  })

  const chartOptions = computed(() => ({
    responsive: true,
    barPercentage: 0.5,
    categoryPercentage: 0.5,
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
            if (context.index === datasetOne.data.length - 1) {
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
        display: false,
      },
    },
  }))

  const { barChartProps, barChartRef } = useBarChart({
    chartData,
    options: chartOptions,
    height: '100%',
    width: '100%',
  })

  onMounted(() => {
    const radius = statCircle.value.r.baseVal.value
    circumference.value = radius * 2 * Math.PI
    strokeDasharray.value = `${circumference.value} ${circumference.value}`
    requestAnimationFrame(updateProgress)

    ctx.value = barChartRef.value.chartInstance.ctx
    gradientOne.value = ctx.value.createLinearGradient(
      0,
      0,
      0,
      ctx.value.canvas.height
    )

    gradientOne.value.addColorStop(0, 'rgba(251, 192, 238, 1)')
    gradientOne.value.addColorStop(0.8, 'rgba(240, 212, 255, 1)')

    gradientTwo.value = ctx.value.createLinearGradient(
      0,
      0,
      0,
      ctx.value.canvas.height
    )
    gradientTwo.value.addColorStop(0, 'rgba(122, 133, 249, 1)')
    gradientTwo.value.addColorStop(1, 'rgba(122, 133, 249, 0.5)')
    barChartRef.value.update()
  })
</script>

<style lang="scss" scoped></style>
