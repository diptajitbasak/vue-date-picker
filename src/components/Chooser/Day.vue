<template lang="pug">
  .day-chooser
    table
      tr
        th(v-for="day in days") {{ day | singleCharacter }}
      tr(v-for="week in (monthCalendar.length / 7)")
        td(v-for="day in 7" @click="updateDay(monthCalendar[(week - 1) * 7 + day - 1], week)" class="yellow" :class="{blue: (week === 1 && monthCalendar[day - 1] > 20) || ((monthCalendar.length / 7) === week && monthCalendar[(week - 1) * 7 + day - 1] < 20), red: day === 7 || day === 1}") {{ monthCalendar[(week - 1) * 7 + day - 1] | doubleCharacter }}
</template>

<script>
import { eventBus } from '../../main'
import { getMonthCalendar } from '../helper'
import { days } from '../constants'

export default {
  data () {
    return {
      days: days,
      scopedDay: this.day,
      scopedMonth: this.month
    }
  },
  props: {
    day: Number,
    month: Number,
    year: Number,
    first: Boolean
  },
  created () {
    eventBus.$on('update:day-1', (value) => {
      this.scopedDay = value
    })
    eventBus.$on('update:day-2', (value) => {
      this.scopedDay = value
    })
    eventBus.$on('update:month-1', (value) => {
      this.scopedMonth = value
    })
    eventBus.$on('update:month-2', (value) => {
      this.scopedMonth = value
    })
  },
  methods: {
    updateDay (value, week) {
      console.log(this.first)
      if (week === 1 && value > 20) {
        this.scopedDay = value
        if (this.scopedMonth === 0) {
          this.scopedMonth = 11
        } else {
          this.scopedMonth = this.scopedMonth - 1
        }
        if (this.first) {
          eventBus.$emit('update:day-1', this.scopedDay)
          eventBus.$emit('update:month-1', this.scopedMonth)
        } else {
          eventBus.$emit('update:day-2', this.scopedDay)
          eventBus.$emit('update:month-2', this.scopedMonth)
        }
      } else if ((week === 5 && value < 20) || (week === 6 && value < 20)) {
        this.scopedDay = value
        if (this.scopedMonth === 11) {
          this.scopedMonth = 0
        } else {
          this.scopedMonth = this.scopedMonth + 1
        }
        if (this.first) {
          eventBus.$emit('update:day-1', this.scopedDay)
          eventBus.$emit('update:month-1', this.scopedMonth)
        } else {
          eventBus.$emit('update:day-2', this.scopedDay)
          eventBus.$emit('update:month-2', this.scopedMonth)
        }
      } else {
        this.scopedDay = value
        if (this.first) {
          eventBus.$emit('update:day-1', this.scopedDay)
        } else {
          eventBus.$emit('update:day-2', this.scopedDay)
        }
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
