<template>
  <div>
    <label> {{radioTitle}} </label>
    <input type="radio" value="0" v-model="defaultRadioVal"/>
    <label>png </label>
    <input type="radio" value="1" v-model="defaultRadioVal"/>
    <label>jpeg </label>
    <input type="radio" value="2" v-model="defaultRadioVal"/>
    <label>svg </label>
  </div>
</template>

<script>
export default {
  name: "A_Radio",
  props: {
    radioTitle: String,
    defaultVal: String,
    vals: [],
    labels: [],
  },
  data: function() {
    return{
      defaultRadioVal: this.defaultVal,
    }
  },
  watch: {
    defaultRadioVal: function(val) {
      // TODO //
      console.log("watch",val)
    }
  }
}
</script>

<style>
</style>
