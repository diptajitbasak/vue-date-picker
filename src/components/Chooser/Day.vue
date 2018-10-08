<template lang="pug">
  .day-chooser
    table
      tr
        th(v-for="day in days") {{ day | singleCharacter }}
      tr(v-for="week in (monthCalendar.length / 7)")
        td(v-for="day in 7" @click="updateDay(monthCalendar[(week - 1) * 7 + day - 1], week)" class="yellow" :class="{blue: (week === 1 && monthCalendar[day - 1] > 20) || ((monthCalendar.length / 7) === week && monthCalendar[(week - 1) * 7 + day - 1] < 20), red: day === 7 || day === 1}") {{ monthCalendar[(week - 1) * 7 + day - 1] | doubleCharacter }}
</template>

<script>
import { getMonthCalendar } from '../helper'
import { days } from '../constants'

export default {
  data () {
    return {
      days: days,
      scopedDay: this.day
    }
  },
  props: {
    day: Number,
    month: Number,
    year: Number
  },
  methods: {
    updateDay (value, week) {
      if (week === 1 && value > 20) {
        this.$emit('previous:month', value)
      } else if ((week === 5 && value < 20) || (week === 6 && value < 20)) {
        this.$emit('next:month', value)
      } else {
        this.scopedDay = value
        this.$emit('update:day', value)
      }
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
.yellow
  background: yellow
.red
  color: red
.blue
  color: blue
</style>
