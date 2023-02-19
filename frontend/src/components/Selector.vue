<template>
    <div>
    <select 
        @change="select" 
        v-model="selected"
    >
        <option v-for="(size, key) in sizeList" :key="key"> 
            {{ size }}
        </option>
    </select>
    </div>
</template>

<script>
export default {
    name: "A_Selecter",
    props: {
        defaultVal             : String,
        selectEl               : Function,
        optionList             : Array,
    }, 
    data: function(){
        return{
            selected           : null,
            sizeList           : this.optionList,
        }
    },
    methods: {
        select(){
            this.selectEl(this.selected)
        }

    }
}
</script>


<style>
</style>