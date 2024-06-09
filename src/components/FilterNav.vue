<template>
  <div class="filter-nav">
    <button @click="filterBy('all')" :class="{active : current === 'all'}">all</button>
    <button @click="filterBy('complete')" :class="{active : current === 'complete'}">complete</button>
    <button @click="filterBy('ongoing')" :class="{active : current === 'ongoing'}">ongoing</button>
  </div>
</template>

<script>
export default {
    props : ['current'],
    methods:{
        filterBy(value){
            this.$emit("filterValue",value)
        }
    }   
}
</script>

<style>
.filter-nav button{
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase; 
}
button.active{
    color:#000000;
    font-weight: bold;
}
</style>