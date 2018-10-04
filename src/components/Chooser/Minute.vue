<template lang="pug">
  .minute-chooser
    .current-time(@click='setCurrentTime') {{ scopedMinute }}
    .numbers
      .minute(v-for="i in 12")
         span(:class="{selected: (5 * (i - 1)) === scopedMinute || (5 * (i - 1)) === scopedMinute - (scopedMinute % 5)}",  @click="setMinute(5 * (i- 1))") {{ (5 * (i - 1)) }}
</template>

<script>
export default {
  props: {
    minute: Number
  },
  data () {
    return {
      scopedMinute: this.minute
    }
  },
  mounted () {
    this.$el.addEventListener('wheel', (event) => {
      if (event.deltaY > 0) {
        if (this.scopedMinute >= 59) {
          this.scopedMinute = 0
        } else {
          this.scopedMinute += 1
        }
      } else {
        if (this.scopedMinute <= 0) {
          this.scopedMinute = 59
        } else {
          this.scopedMinute -= 1
        }
      }
      this.$emit('update:minute', this.scopedMinute)
    })
  },
  destroyed () {
    this.$el.removeEventListener('wheel', null)
  },
  methods: {
    setMinute (value) {
      this.$emit('set-minute', value)
    },
    setCurrentTime () {
      console.log('hello')
    }
  }
}
</script>

<style lang="sass" scoped>
$radius: 100px
.minute-chooser
  position: relative
  .current-time
    position: absolute
    transform: translateY($radius) translate(-50%, -50%)
  .numbers
    .minute
      height: $radius
      position: absolute
      top: 0
      left: 0
      transform-origin: 0 100%
      @for $minute from 1 through 12
        &:nth-child(#{$minute})
          transform: rotate(#{30 * ($minute - 1)}deg)
      .selected
        position: relative
        background: blue
        color: white
</style>
