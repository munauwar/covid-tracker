<template>
  <Chart
    :size="{ width: 500, height: 420 }"
    :data="dataGraph"
    :margin="margin"
    :direction="direction"
    :axis="axis">

  </Chart>
</template>

<script>
import { defineComponent, ref } from 'vue'
import { Chart, Grid, Line } from 'vue3-charts'

export default defineComponent({
  name: 'Graphs',
  props: ["dataGraph"],
  components: { Chart, Grid, Line },
  setup() {
    // const data = ref(plByMonth)
    const direction = ref('horizontal')
    const margin = ref({
      left: 0,
      top: 20,
      right: 20,
      bottom: 0
    })

    const axis = ref({
      primary: {
        type: 'band'
      },
      secondary: {
        domain: ['dataMin', 'dataMax + 100'],
        type: 'linear',
        ticks: 8
      }
    })

    return { direction, margin, axis }
  }
})
</script>