<template lang="pug">
  div(class="icon" @click="openDropdown = !openDropdown") Q
    div(class="dropdown" v-if="openDropdown")
      div(@click="setLastMonth") Last Month
      div(@click="setSixMonth") Last 6 Month
      div(@click="setYesterday") Yesterday
      div(@click="setTomorrow") Tomorrow
      div(@click="setLastHour") Last Hour
</template>

<script>
import { getMonthCalendar } from './helper'

export default {
  props: {
    timeStart: Object,
    timeEnd: Object
  },
  data () {
    return {
      openDropdown: false,
      scopedTimeStart: this.timeStart,
      scopedTimeEnd: this.timeEnd
    }
  },
  methods: {
    setTomorrow () {
      let daysInMonth = getMonthCalendar(this.scopedTimeStart.month, this.scopedTimeStart.year)
      let day = new Date().getDate()
      function findTheDate (element) {
        return element === day
      }
      let position = daysInMonth.findIndex(findTheDate)
      if (daysInMonth[position] > daysInMonth[position + 1]) {
        this.scopedTimeStart.month = this.scopedTimeStart.month + 1
        this.scopedTimeStart.day = daysInMonth[position + 1]
      } else {
        this.scopedTimeStart.day = daysInMonth[position + 1]
      }
    },
    setYesterday () {
      let daysInMonth = getMonthCalendar(this.scopedTimeStart.month, this.scopedTimeStart.year)
      let day = new Date().getDate()
      function findTheDate (element) {
        return element === day
      }
      let position = daysInMonth.findIndex(findTheDate)
      if (daysInMonth[position] < daysInMonth[position - 1]) {
        this.scopedTimeStart.month = this.scopedTimeStart.month - 1
        this.scopedTimeStart.day = daysInMonth[position - 1]
      } else {
        this.scopedTimeStart.day = daysInMonth[position - 1]
      }
    },
    setLastMonth () {
      let month = new Date().getMonth()
      this.scopedTimeStart.month = month - 1
    },
    setSixMonth () {
      let month = new Date().getMonth()
      let lastSixMonth = [7, 8, 9, 10, 11, 12]
      let firstSixMonth = [1, 2, 3, 4, 5, 6]
      if (lastSixMonth.includes(month)) {
        this.scopedTimeStart.month = (month - 6)
      }
      if (firstSixMonth.includes(month)) {
        this.scopedTimeStart.month = (month + 6)
      }
    },
    setLastHour () {
      let hour = new Date().getHours()
      this.scopedTimeStart.hour = hour - 1
    }
  }
}
</script>

<style lang="sass" scoped>
.icon
  position: relative
  .dropdown
    position: absolute
    width: 100px
    background: red
</style>
