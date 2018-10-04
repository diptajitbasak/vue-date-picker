<template lang="pug">
  .date-picker
    custom-input(:value="formattedValue")
    chooser(:options="options" :time="start")
    chooser(v-if="options.range" :options="options" :time="end")
</template>

<script>
import CustomInput from './CustomInput'
import Chooser from './Chooser'

const now = new Date()

export default {
  props: {
    options: Object
  },
  components: {
    CustomInput,
    Chooser
  },
  data () {
    return {
      start: {
        day: now.getDate(),
        month: now.getMonth(),
        year: now.getFullYear(),
        hour: now.getHours(),
        minute: now.getMinutes(),
        second: now.getSeconds()
      },
      end: {
        day: now.getDate(),
        month: now.getMonth(),
        year: now.getFullYear(),
        hour: now.getHours(),
        minute: now.getMinutes(),
        second: now.getSeconds()
      }
    }
  },
  computed: {
    formattedValue () {
      // Fill this up
      return ''
    }
  }
}
</script>

<style lang="sass" scoped>
</style>
