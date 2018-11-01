<template lang="pug">
  .chooser
    template(v-if="options.chooser.includes('day')")
      day(:month="time.month" :year="time.year" :day.sync="time.day" :first="first")
    template(v-if="options.chooser.includes('month')")
      month(:month.sync="time.month" :first="first")
    template(v-if="options.chooser.includes('year')")
      year(:year.sync="time.year" :first="first")
    template(v-if="options.chooser.includes('hour')")
      hour(class="hour" :hour.sync="time.hour" :first="first")
    template(v-if="options.chooser.includes('minute')")
      minute(class="minute" :minute.sync="time.minute" :first="first")
    template(v-if="options.chooser.includes('second')")
      second(class="second" :second.sync="time.second" :first="first")
</template>

<script>
import Day from './Day'
import Month from './Month'
import Year from './Year'
import hour from './Hour'
import minute from './Minute'
import second from './Second'

export default {
  props: {
    options: Object,
    time: Object,
    first: Boolean
  },
  components: {
    Day,
    Month,
    Year,
    hour,
    minute,
    second
  }
}
</script>

<style lang="sass" scoped>
</style>
