<template>
  <div id="app">
<h1> BLOG</h1>
<div>{{htmls}}</div>

 </div>
</template>

<script>

export default {  
  

  data() {
      console.log('hello')
      console.log(this.$route.params)
      
    return {
      
      htmls : this.$route.params['data'],

  

    };
  },
methods:{
  // created(){
  //   this.$http.get('http://localhost:4000/api/blog/').then(function(data){
  //     console.log(data.body)
  //     })
  }
}

</script>

<style>
#app {
  font-size: 18px;
  font-family: 'Roboto', sans-serif;
  color: blue;
}
</style>