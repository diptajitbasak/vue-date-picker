<template lang="pug">
  div(class="icon" @click="openDropdown = !openDropdown") Q
    div(class="dropdown" v-if="openDropdown")
      div(class="item" @click="setLastMonth") last Month
</template>

<script>
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
    setLastMonth () {
      this.scopedTimeStart.month = this.scopedTimeStart.month - 1
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
