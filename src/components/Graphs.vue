<template>
  <Chart
    :size="{ width: 500, height: 400 }"
    :data="data"
    :margin="margin"
    :direction="direction">

    <template #layers>
      <Grid strokeDasharray="2,2" />
      <Line :dataKeys="['name', 'pl']" />
    </template>

  </Chart>
</template>

<script>
import { defineComponent, ref } from 'vue'
import { Chart, Grid, Line } from 'vue3-charts'

export default defineComponent({
  name: 'LineChart',
  props: ['data'],
  components: { Chart, Grid, Line },
  setup() {
    // const data = ref(data)
    const direction = ref('horizontal')
    const margin = ref({
      left: 0,
      top: 20,
      right: 20,
      bottom: 0
    })

    return { direction, margin }
  }
})
</script>
