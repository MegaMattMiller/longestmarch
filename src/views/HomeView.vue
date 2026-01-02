<template>
  <div class="wrapper">
    <h1>It is currently March {{ numberWithCommas(daysSince) }}{{ nth(daysSince) }}, 2020</h1>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const daysSince = computed(() => {
  const startDate = new Date('2020-03-13')
  const currentDate = new Date()
  const diffTime = Math.abs(currentDate.getTime() - startDate.getTime())
  const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24))
  return diffDays + 13
})

function nth(d: number) {
  const dString = String(d)
  const last = +dString.slice(-2)
  if (last > 3 && last < 21) return 'th'
  switch (last % 10) {
    case 1:
      return 'st'
    case 2:
      return 'nd'
    case 3:
      return 'rd'
    default:
      return 'th'
  }
}

function numberWithCommas(x: number) {
  return x.toString().replace(/\B(?<!\.\d*)(?=(\d{3})+(?!\d))/g, ',')
}
</script>
