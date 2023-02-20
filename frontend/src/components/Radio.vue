<template>
  <div>
    <label> {{ radioTitle }} </label>
    <span v-for="key in keys" :key="key">
      <input type="radio" :value="vals[key]" :key="key" v-model="defaultRadioVal"/>
      <label> {{ labels[key] }} </label>
    </span>

  </div>
</template>

<script>
export default {
  name: "A_Radio",
  props: {
    radioTitle: String,
    defaultVal: String,
    keys: [],
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
