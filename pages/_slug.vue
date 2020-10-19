<template>
<div class="container blog__container">
<h1 class="header_text">{{info.blog_title}}</h1>
<img  class="img_res" v-bind:src="imgurl"/>
<p v-html="info.keywords"></p>
<p class="des_image" v-html="info.blog_description">

  

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

      imgurl:""

    };
  },
      methods:{
        arrayBufferToBase64(buffer) {
          var binary = '';
          var bytes = [].slice.call(new Uint8Array(buffer));
          bytes.forEach((b) => binary += String.fromCharCode(b));
          return window.btoa(binary);
      },
      },
  async mounted(){
   let res = await axios
  .get(' http://localhost:4000/api/blog/p/'+this.slug)
    let base64Flag = 'data:image/jpeg;base64,';
    let imgString = this.arrayBufferToBase64(res.data.blog_image.data.data)
    this.info = res.data
    this.imgurl = `${base64Flag}${imgString}`
   },
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

  font-size:48px;
  font-family: medium-content-title-font, Georgia, Cambria, "Times New Roman", Times, serif;
  margin-left:30%;
  margin-right:30%
  }
.blog__container p {
  width: 50%
}
.img_res{
  height:50%x;
  width:40%
}
.des_image img {
   max-height: -webkit-fill-available;
   margin-top: 70px;
   width: 200%;
}

.blog__container p::first-letter {
  font-size: 200%;
  font-weight: bolder
}
</style>