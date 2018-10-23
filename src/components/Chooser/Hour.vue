<template lang="pug">
  div(class="hour-picker")
    .hour-chooser
      .current-time {{ scopedHour }}
      .numbers
        .hour(v-for="i in 24")
          span(:class="{selected: (i - 1) === scopedHour}", @click="setHour( i- 1 )") {{ i - 1 }}
</template>

<script>

export default {
  props: {
    hour: Number
  },
  data () {
    return {
      scopedHour: this.hour
    }
  },
  methods: {
    setHour (value) {
      this.scopedHour = value
      this.$emit('update:hour', this.scopedHour)
    }
  },
  mounted () {
    this.$el.addEventListener('wheel', (event) => {
      if (event.deltaY > 0) {
        if (this.scopedHour === 23) {
          this.scopedHour = 0
        } else {
          this.scopedHour += 1
        }
      } else {
        if (this.scopedHour === 0) {
          this.scopedHour = 23
        } else {
          this.scopedHour -= 1
        }
      }
      this.$emit('update:hour', this.scopedHour)
    })
  },
  destroyed () {
    this.$el.removeEventListener('wheel', this.scopedHour)
  }
}
</script>

<style lang="sass" scoped>
$radius: 100px
.hour-picker
  height: 210px
  width: 200px
  .hour-chooser
    position: relative
    .current-time
      position: absolute
      transform: translateY($radius) translate(-50%, -50%)
    .numbers
      .hour
        height: $radius
        position: absolute
        top: 0
        left: 0
        transform-origin: 0 100%
        @for $hour from 1 through 24
          &:nth-child(#{$hour})
            transform: rotate(#{15 * ($hour - 1)}deg)
        .selected
          position: relative
          background: blue
          color: white
</style>
