<template>
<div class="container blog__container">
<h1 class="header_text">{{info.blog_title}}</h1>
<img  class="img_res" v-bind:src="url + info.blog_image"/>
<p v-html="info.blog_description">

  

  </p>
 </div>
</template>

<script>
import axios from 'axios'

export default {  
  // layout:"topnavbar",
  

  data() {
      console.log('hello')
      console.log(this.$route.params)
      
    return {
      info:"",
      slug : this.$route.params['slug'],

      url:'http://localhost:4000'

    };
  },
  mounted(){
    console.log(this.htmls,"htmsmsmsm")
   axios
  .get(' http://localhost:4000/api/blog/p/'+this.slug)
  .then(response => (this.info = response.data))
   },
methods:{
}
}
</script>

<style>
.blog__container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  
}
.header_text{
  margin-top:30px;
  font-size:48px;
  font-family: medium-content-title-font, Georgia, Cambria, "Times New Roman", Times, serif;
  margin-left:30%;
  margin-right:30%
  }
.blog__container p {
  width: 50%
}
.blog__container p::first-letter {
  font-size: 200%;
  font-weight: bolder
}
</style>