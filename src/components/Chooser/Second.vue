<template lang="pug">
  div(class="second-picker")
    .second-chooser
      .current-time {{ scopedSecond }}
      .numbers
        .second(v-for="i in 12")
          span(:class="{selected: (5 * (i - 1)) === scopedSecond || (5 * (i - 1)) === scopedSecond - (scopedSecond % 5)}",  @click="setSecond(5 * (i- 1))") {{ (5 * (i - 1)) }}
</template>

<script>
export default {
  props: {
    second: Number
  },
  data () {
    return {
      scopedSecond: this.second
    }
  },
  methods: {
    setSecond (value) {
      this.scopedSecond = value
      this.$emit('update:second', this.scopedSecond)
    }
  },
  mounted () {
    this.$el.addEventListener('wheel', (event) => {
      if (event.deltaY > 0) {
        if (this.scopedSecond >= 59) {
          this.scopedSecond = 0
        } else {
          this.scopedSecond += 1
        }
      } else {
        if (this.scopedSecond <= 0) {
          this.scopedSecond = 59
        } else {
          this.scopedSecond -= 1
        }
      }
      this.$emit('update:second', this.scopedSecond)
    })
  },
  destroyed () {
    this.$el.removeEventListener('wheel', null)
  }
}
</script>

<style lang="sass" scoped>
$radius: 100px
.second-picker
  height: 210px
  width: 200px
  .second-chooser
    position: relative
    .current-time
      position: absolute
      transform: translateY($radius) translate(-50%, -50%)
    .numbers
      .second
        height: $radius
        position: absolute
        top: 0
        left: 0
        transform-origin: 0 100%
        @for $second from 1 through 12
          &:nth-child(#{$second})
            transform: rotate(#{30 * ($second - 1)}deg)
        .selected
          position: relative
          background: blue
          color: white
</style>
