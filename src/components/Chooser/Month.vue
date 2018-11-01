<template lang="pug">
  .month-chooser
    ul
      li(v-for="i in 7" @click="setMonth((scopedMonth + i - 1) % 12)") {{ months[(scopedMonth + i - 1) % 12] }}
</template>

<script>
import { eventBus } from '../../main'
import { months } from '../constants'

export default {
  props: {
    month: Number,
    first: Boolean
  },
  data () {
    return {
      months: months,
      scopedMonth: this.month
    }
  },
  methods: {
    setMonth (value) {
      this.scopedMonth = value
      if (this.first) {
        eventBus.$emit('update:month-1', this.scopedMonth)
      } else {
        eventBus.$emit('update:month-2', this.scopedMonth)
      }
    }
  },
  mounted () {
    this.$el.addEventListener('wheel', (event) => {
      if (event.deltaY > 0) {
        this.scopedMonth = (this.scopedMonth + 1) % 12
      } else {
        this.scopedMonth = (this.scopedMonth + 11) % 12
      }
      if (this.first) {
        eventBus.$emit('update:month-1', this.scopedMonth)
      } else {
        eventBus.$emit('update:month-2', this.scopedMonth)
      }
    })
  },
  destroyed () {
    this.$el.removeEventListener('wheel', null)
  }
}
</script>

<style lang="sass" scoped>
ul
  list-style-type: none
  li:nth-child(1)
    font-size: 30px
</style>
