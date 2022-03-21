<template>
  <Chart
    :size="{ width: 500, height: 400 }"
    :data="data"
    :margin="margin"
    :direction="direction">

    <template #layers>
      <Grid strokeDasharray="2,2" />
      <Bar :dataKeys="['barName1', 'barValue1']" :barStyle="{fill: '#90e0ef'}" />
      <Bar :dataKeys="['barName2', 'barValue2']" :barStyle="{fill: '#70e0ef'}" />
    </template>

  </Chart>
</template>

<script>
import { defineComponent, ref } from 'vue'
import { Chart, Grid, Bar } from 'vue3-charts'

export default defineComponent({
  name: 'Graphs',
  props: ['data'],
  components: { Chart, Grid, Bar },
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
