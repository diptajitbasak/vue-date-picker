<template lang="pug">
  div(class="icon" @click="openDropdown = !openDropdown") Q
    div(class="dropdown" v-if="openDropdown")
      div(@click="setLastMonth") Last Month
      div(@click="setYesterday") Yesterday
      div(@click="setTomorrow") Tomorrow
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
    setYesterday () {
      // console.log(this.scopedTimeStart.day)
    },
    setTomorrow () {
      let daysInMonth = getMonthCalendar(this.scopedTimeStart.month, this.scopedTimeStart.year)
      console.log(daysInMonth)
    },
    setLastMonth () {
      if (this.scopedTimeStart.month === 0) {
        this.scopedTimeStart.month = 11
        this.scopedTimeStart.year = this.scopedTimeStart.year - 1
      } else {
        this.scopedTimeStart.month = this.scopedTimeStart.month - 1
      }
      console.log(this.scopedTimeStart.month)
      console.log(this.scopedTimeStart.year)
      this.$emit('update:month', this.scopedTimeStart.month)
    }
  }
}
</script>

<style lang="sass" scoped>
.icon
  position: relative
  .dropdown
    position: absolute
    // position: relative
    width: 100px
    background: red
</style>
