<template>
  <span>
    <button id="btnel" @click="pushBtn"> 
      {{ btnLabel }} 
    </button>
  </span>
</template>

<script>
export default {
  name: "A_Button",
  props: {
    tag: String,
    btnLabel: String,
    pushBtn: Function, 
  },
}
</script>

<style scoped>
#btnel {
    color: #333333 ;
    background-color: #EFEFEF;
    border-radius: 1px 1px 1px 1px;
    cursor: pointer;
}
</style>
