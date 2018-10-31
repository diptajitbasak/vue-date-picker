<template lang="pug">
  .date-picker
    custom-input(class='input' :value="formattedValue" :label="options.label")
    quick-pick(class='quick-pick' v-if="options.quickPick" :timeStart="start" :timeEnd="end")
    chooser(class='chooser-1' :options="options" :time="start")
    chooser(class='chooser-2' v-if="options.range" :options="options" :time="end")
</template>

<script>
import { eventBus } from '../main'
import CustomInput from './CustomInput'
import Chooser from './Chooser'
import QuickPick from './QuickPick'

import { format } from './helper'

const now = new Date()

export default {
  props: {
    options: Object
  },
  components: {
    CustomInput,
    Chooser,
    QuickPick
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
  created () {
    eventBus.$on('update:day', (value) => {
      this.start.day = value
    })
    eventBus.$on('update:month', (value) => {
      this.start.month = value
    })
    eventBus.$on('update:year', (value) => {
      this.start.year = value
    })
  },
  computed: {
    formattedValue () {
      const dateOptions = ['day', 'month', 'year'].filter(e => this.options.chooser.includes(e))
      const timeOptions = ['hour', 'minute', 'second'].filter(e => this.options.chooser.includes(e))

      const startDate = dateOptions
        .map(e => (e === 'month') ? (this.start[e] + 1) : this.start[e])
        .map(e => format(e, '0', 2))
        .join('/')
      const startTime = timeOptions.map(e => format(this.start[e], '0', 2)).join(':')

      if (!this.options.range) {
        return `${startDate} ${startTime}`
      }

      const endDate = dateOptions
        .map(e => (e === 'month') ? (this.end[e] + 1) : this.end[e])
        .map(e => format(e, '0', 2))
        .join('/')
      const endTime = timeOptions.map(e => format(this.end[e], '0', 2)).join(':')

      return `${startDate} ${startTime} - ${endDate} ${endTime}`
    }
  }
}
</script>

<style lang="sass" scoped>
.date-picker
  display: grid
  grid-template-column: 1fr 1fr 1fr
  grid-gap: 10px
  .input
    grid-column: 1/3
  .quick-pick
    grid-column: 3/4
  .chooser-1
    grid-column: 1
  .chooser-2
    grid-column: 2
</style>
