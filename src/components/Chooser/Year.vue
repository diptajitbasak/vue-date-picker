<template lang="pug">
  .year-chooser
    ul
      li(v-for="i in 9" @click='setYear(scopedYear + i - 1)') {{ scopedYear + i - 1 }}
</template>

<script>
import { eventBus } from '../../main'

export default {
  props: {
    year: Number,
    first: Boolean
  },
  data () {
    return {
      scopedYear: this.year
    }
  },
  methods: {
    setYear (value) {
      this.scopedYear = value
      if (this.first) {
        eventBus.$emit('update:year-1', this.scopedYear)
      } else {
        eventBus.$emit('update:year-2', this.scopedYear)
      }
    }
  },
  mounted () {
    this.$el.addEventListener('wheel', (event) => {
      if (event.deltaY > 0) {
        this.scopedYear += 1
      } else {
        this.scopedYear -= 1
      }
      if (this.first) {
        eventBus.$emit('update:year-1', this.scopedYear)
      } else {
        eventBus.$emit('update:year-2', this.scopedYear)
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
