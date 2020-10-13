<template>
  <div id="app">
<h1> BLOG</h1>
<div>{{info}}</div>
{{info}}
 </div>
</template>

<script>
import axios from 'axios'

export default {  
  

  data() {
      console.log('hello')
      console.log(this.$route.params)
      
    return {
      
      htmls : this.$route.params['slug'],

  

    };
  },
  mounted(){
   axios
  .get(' http://localhost:4000/api/blog/p/'+slug)
  .then(response => (this.info = response))
   },
methods:{
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