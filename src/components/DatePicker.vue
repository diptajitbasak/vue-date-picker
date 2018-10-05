<template lang="pug">
  .date-picker
    custom-input(class='input' :value="formattedValue")
    chooser(class='chooser-1' :options="options" :time="start")
    chooser(class='chooser-2' v-if="options.range" :options="options" :time="end")
</template>

<script>
import CustomInput from './CustomInput'
import Chooser from './Chooser'

const now = new Date()

export default {
  props: {
    options: Object
  },
  components: {
    CustomInput,
    Chooser
  },
  data () {
    return {
      start: {
        day: now.getDate(),
        month: now.getMonth(),
        year: now.getFullYear(),
        hour: now.getHours(),
        minute: now.getMinutes(),
        second: now.getSeconds()
      },
      end: {
        day: now.getDate(),
        month: now.getMonth(),
        year: now.getFullYear(),
        hour: now.getHours(),
        minute: now.getMinutes(),
        second: now.getSeconds()
      }
    }
  },
  computed: {
    formattedValue () {
      // Fill this up
      let startDay = this.start.day
      let startMonth = this.start.month
      let startYear = this.start.year
      return `${startDay}/${startMonth}/${startYear}`
    }
  }
}
</script>

<style lang="sass" scoped>
.date-picker
  display: grid
  grid-template-column: 1fr 1fr
  grid-gap: 10px
  .input
    grid-column: 1/3
  .chooser-1
    grid-column: 1
  .chooser-2
    grid-column: 2
</style>
