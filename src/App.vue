<template lang="pug">
  #app
    //- custom-input
    date-picker(:options="{chooser:['hour']}")
</template>

<script>
import DatePicker from './components/DatePicker'
// import CustomInput from './components/CustomInput'

export default {
  name: 'app',
  components: {
    DatePicker
    // CustomInput
  }
}
</script>

<style lang="sass">
#app
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  color: #2c3e50
  margin-top: 60px
  margin-left: 300px
  margin-right: 300px
</style>
