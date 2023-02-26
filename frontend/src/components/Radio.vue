<template>
  <div>
    <label> {{ radioTitle }} </label>
    <span v-for="key in keys" :key="key">
      <input type="radio" :value="vals[key]" :key="key" v-model="selectedVal"/>
      <label> {{ labels[key] }} </label>
    </span>

  </div>
</template>

<script>
export default {
  name: "A_Radio",
  props: {
    radioTitle: String,
    radioVal: String,
    setVal: Function, 
    keys: [],
    vals: [],
    labels: [],
  },
  data: function() {
    return{
      selectedVal: this.radioVal,
    }
  },
  watch: {
    selectedVal: function(val) {
      this.setVal(val)
    }
  }
}
</script>

<style>
</style>
