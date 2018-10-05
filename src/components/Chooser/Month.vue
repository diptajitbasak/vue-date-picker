<template lang="pug">
  .month-chooser
    ul
      li(v-for="i in 7") {{ months[(scopedMonth + i - 1) % 12] }}
</template>

<script>
import { months } from '../constants'

export default {
  props: {
    month: Number
  },
  data () {
    return {
      months: months,
      scopedMonth: this.month
    }
  },
  mounted () {
    this.$el.addEventListener('wheel', (event) => {
      if (event.deltaY > 0) {
        this.scopedMonth = (this.scopedMonth + 1) % 12
      } else {
        this.scopedMonth = (this.scopedMonth + 11) % 12
      }
      this.$emit('update:month', this.scopedMonth)
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
