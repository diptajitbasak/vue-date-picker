<template lang="pug">
  div
    .day-chooser
      table
        tr
          th(v-for="day in days") {{ day | singleCharacter }}
        tr(v-for="week in (monthCalendar.length / 7)")
          td(v-for="day in 7" @click="updateDay(monthCalendar[(week - 1) * 7 + day - 1])") {{ monthCalendar[(week - 1) * 7 + day - 1] | doubleCharacter }}
</template>

<script>
import { getMonthCalendar } from './helper'
export default {
  props: {
    month: Number,
    year: Number
  },
  data () {
    return {
      days: ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']
    }
  },
  methods: {
    updateDay (value) {
      this.$emit('update:day', value)
    }
  },
  computed: {
    monthCalendar () {
      return getMonthCalendar(this.month, this.year)
    }
  },
  filters: {
    singleCharacter (value) {
      return value.slice(0, 1)
    },
    doubleCharacter (value) {
      let valueStr = value.toString()
      if (valueStr.length === 1) {
        return 0 + valueStr
      } else {
        return value
      }
    }
  }
}
</script>

<style lang="sass" scoped>
</style>
