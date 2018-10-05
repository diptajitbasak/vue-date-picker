<template lang="pug">
  .chooser
    template(v-if="options.chooser.includes('day')")
      day(:month="time.month" :year="time.year")
    template(v-if="options.chooser.includes('month')")
      month(:month.sync="time.month")
    template(v-if="options.chooser.includes('year')")
      year(:year.sync="time.year")
    template(v-if="options.chooser.includes('hour')")
      hour(class="hour" :hour.sync="time.hour")
    template(v-if="options.chooser.includes('minute')")
      minute(class="minute" :minute.sync="time.minute")
    template(v-if="options.chooser.includes('second')")
      second(class="second" :second.sync="time.second")
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
    time: Object
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
