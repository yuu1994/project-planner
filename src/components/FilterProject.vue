<template>
  <div class="filter-nav">
    <button @click="currentValue('all')" :class="{current:current=='all'}">all</button>
    <button @click="currentValue('complete')" :class="{current:current=='complete'}">Complete</button>
    <button @click="currentValue('ongoing')" :class="{current:current=='ongoing'}">Ongoing</button>
  </div>
</template>
<script>
export default {
    props : ['current'],
    methods: {
        currentValue(value){
            this.$emit('currentValue',value)
            // console.log(value)
        }
    }
};
</script>
<style scoped>
.filter-nav {
    display: flex;
}
button {
    background-color: white;
    color: gray;
    text-transform: capitalize;
    border-radius: 0;
}
button:hover {
    background-color: white;
    color: rgb(104, 101, 101);
}
.current {
    border-bottom: 3px solid green;
    color: rgb(104, 101, 101);
    padding-bottom: 6px;
}
</style>
