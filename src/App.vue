<template>
  <div id="app">
    
 <app-weather></app-weather>
  </div>
</template>

<script>
import Weather from './Weather.vue';
export default {
  
  components:{
    'app-weather':Weather
  }
}
</script>

<style lang="css" >
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
</style>


