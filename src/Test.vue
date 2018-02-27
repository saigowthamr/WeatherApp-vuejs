<template>
  <div>
<h1>HUU AWS </h1> <br> <br>
<button @click="find">Find aws</button>
  </div>
</template>


<script>
export default {
  

  methods:{
    find(){
        var url='https://4d3sjbd7x0.execute-api.us-east-1.amazonaws.com/dev/compare-yourself';
        this.$http.post(url)
        .then((response)=>{
            return response.json()
        }).then(data=>{
            console.log(data)
        })
    }
  }
}
</script>



<style>

</style>
