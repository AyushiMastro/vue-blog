<template>

  <div class="position-relative">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
    <div class="Blog-content">
      <div class>
        <h3>Blog</h3>
      </div>
      <div class="d-flex justify-content-between">
        <p>Create a Blog Post</p>
        <ul class="dashboard">
          <li>Home</li>
          <li>Dashboard</li>
          <li>Add a Blog</li>
        </ul>
      </div>

      <div class="row">
        <div class="col-sm-9">
          <section class="editor-container">
            <quill-editor
              ref="editor"
              v-model="content"
              :options="editorOption"
              @blur="onEditorBlur($event)"
              @focus="onEditorFocus($event)"
              @ready="onEditorReady($event)"
              @change="onEditorChange($event)"
            />
            <div v-if="!blog_image" class="bg-grey">
              <input id="file" type="file" @change="onUpload($event)" />
            </div>
            <div v-else class="image__class">
            <img :src="blog_image_url" />
            </div>
            <br />
            <input field class="in-field" placeholder="HeadLine" @change="onChange"/>
            <br />
            <br/>
            <button @click="controlnav" id ="main_photo" ><i class="fa fa-plus"></i></button>  

              <div class="add_item"  ref="add_content">

                <div id="hide" class="block_items">
                  <button @click="uploadimage" class="all_buttons"><i class="fa fa-image">images</i></button> 
                  <button @click="uploadvideo" class="all_buttons"><i class="fa fa-video-camera">video</i></button> 
                  <button @click="uploadslide" class="all_buttons"><i class="fa fa-slideshare">slides</i></button> 
                  <button @click="uploadlink" class="all_buttons"><i class="fa fa-link">links</i></button>
                  <button @click="snippet_click" class="all_buttons"><i class="fa fa-code">snippet</i></button>  
                </div>
              </div>

              <div class="pick_content" ref="upload_image">
              <input type="file"   class="upload_File" id="selectImg" accept="image/gif, image/jpeg, image/png" @change="image_click"
             multiple/>             
              </div>

              <div class="pick_content" ref="upload_video">
                <input ref="video_link" field class="upload_File" placeholder="Paste the video link "/>
                <button class="submit_Button" @click="video_click">Submit</button>
              </div>

              <div class="pick_content" ref="upload_slide">
                <input ref="slide_link" field class="upload_File" placeholder="Paste the slide link "/>
                <button class="submit_Button" @click="slide_click">Submit</button>
              </div>
                 <div class="pick_content" ref="upload_link">
                <input ref="link_link" field class="upload_File" placeholder="Paste the link "/>
                <button class="submit_Button" @click="link_click">Submit</button>
              </div>

           



          </section>

        </div>
        <div class="col-sm-3">
          <div class="button-box">
            <b-button variant="primary" @click="handleClick"
              >Save and Publish</b-button
            >
          </div>
          <div class="add-field">
            <div>
              <label class="text-label">Tags</label>
              <b-form-input
                v-model="text"
                placeholder="Add Keywords"
                class="add_keywords"></b-form-input>
              <div class="add-outer" @click="onPress">+</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import VueResource from 'vue-resource'
Vue.use(VueResource)
const key_arr = [];
export default {
  name: "quill-example-nuxt",
  data() {
    return {
      editorOption: {
        // Some Quill options...
        theme: "snow",
        modules: {
          toolbar: [
            [
              {
                header: [1, 2, false]               
              }
              
            ],
            ["bold", "italic", "underline"],
            ["image", "code-block"]
          ]
        }

      },
      blog_description:'',
      blog_title:'',
      blog_image:'',  
      blog_image_url:'',
      img_src:'', 
    };
  },

  methods: {
    onEditorChange(editor){
    this.blog_description = editor.html
    console.log(this.blog_description,"description",editor)
    },
    onChange(e){
      this.blog_title=e.target.value
      console.log(this.blog_title,'title')
    },
    onEditorFocus(editor) {
      console.log("editor focus!", editor);
    },
    onEditorReady(editor) {
      console.log("editor ready!", editor);
      },
      onPress(){
        var keywrd = document.getElementById("__BVID__17").value ;
        key_arr.push(keywrd)
        console.log(key_arr)
      },

      controlnav(){
      var x = this.$refs["add_content"];
      if (x.style.display === "none") 
      {
        x.style.display = "inline-block";
      } 
      else {
      x.style.display = "none";
      var image = this.$refs["upload_image"];       
      var video = this.$refs["upload_video"];
      var slide = this.$refs["upload_slide"];
      var link = this.$refs["upload_link"];
      slide.style.display = "none";
      link.style.display = "none";
      video.style.display = "none";
      image.style.display = "none"; 

       }

      },
           uploadimage(){
      var image = this.$refs["upload_image"];       
      var video = this.$refs["upload_video"];
      var slide = this.$refs["upload_slide"];
      var link = this.$refs["upload_link"];
      slide.style.display = "none";
      link.style.display = "none";
      video.style.display = "none";


      if (image.style.display === "none") 
      {
        image.style.display = "block";  
      } 
      else {
      image.style.display = "none";
       }

      },
      uploadvideo(){
      var image = this.$refs["upload_image"];
      var video = this.$refs["upload_video"];
      var slide = this.$refs["upload_slide"];
      var link = this.$refs["upload_link"];

      image.style.display = "none";
      slide.style.display = "none";
      link.style.display = "none";

      if (video.style.display === "none") 
      {
        video.style.display = "block";  
      } 
      else {
      video.style.display = "none";
       }

      },
      uploadslide(){
      var image = this.$refs["upload_image"];
      var slide = this.$refs["upload_slide"];
      var video = this.$refs["upload_video"];
      var link = this.$refs["upload_link"];

      video.style.display = "none";
      link.style.display = "none";
      image.style.display = "none";


      if (slide.style.display === "none") 
      {
        slide.style.display = "block";
      } 
      else {
      slide.style.display = "none";
       }

      },
       uploadlink(){
      var image = this.$refs["upload_image"];
      var slide = this.$refs["upload_slide"];
      var video = this.$refs["upload_video"];
      var link = this.$refs["upload_link"];

      image.style.display = "none";
      video.style.display = "none";
      slide.style.display = "none";


      if (link.style.display === "none") 
      {
        link.style.display = "block";
      } 
      else {
      link.style.display = "none";
       }

      },


      image_click(){
        console.log('function called image_click')
        var file = document.querySelector('#selectImg').files[0];
        console.log('file',file)
        var reader = new FileReader();
        let src = ""
        reader.addEventListener("load", () => {
        const src = reader.result;
        this.img_src = src
        let quill = this.$refs.editor.quill
        let length = quill.getSelection(true).index;
        quill.insertEmbed(length, 'image', src);
        quill.setSelection(length+=1);

        }, false);

      if (file) {
        reader.readAsDataURL(file);
      }
     
      var image = this.$refs["upload_image"];   
      image.style.display = "none";
      },

      video_click(){
        console.log('video_click',this.$refs.video_link.value)
        var video_input_url = this.$refs.video_link.value
        
        const desc = this.$refs.editor.quill;
        var selection = desc.getSelection(true);
        this.$refs.editor.quill.insertEmbed(selection.index, 'video', video_input_url);   
        this.$refs.editor.quill.setSelection(selection.index+=1);
        var video = this.$refs["upload_video"];
        video.style.display = "none";


      },

      slide_click(){
        console.log('slide_click',this.$refs.slide_link.value)
        var slide_input_url = this.$refs.slide_link.value
        const desc = this.$refs.editor.quill;
        var selection = desc.getSelection(true);
        this.$refs.editor.quill.insertEmbed(selection.index, 'video', slide_input_url);   
        this.$refs.editor.quill.setSelection(selection.index+=1);
        var slide = this.$refs["upload_slide"];
        slide.style.display = "none";
      },
      link_click(){
        console.log('link_click',this.$refs.link_link.value)
        var link_input_url = this.$refs.link_link.value
        const desc = this.$refs.editor.quill;
        var selection = desc.getSelection(true);
        this.$refs.editor.quill.insertEmbed(selection.index, 'video', link_input_url);   
        this.$refs.editor.quill.setSelection(selection.index+=1);
        var link = this.$refs["upload_link"];
        link.style.display = "none";   
       },

      snippet_click(){
      var image = this.$refs["upload_image"];       
      var video = this.$refs["upload_video"];
      var slide = this.$refs["upload_slide"];
      var link = this.$refs["upload_link"];
      slide.style.display = "none";
      link.style.display = "none";
      video.style.display = "none";
      image.style.display = "none"; 
      const desc = this.$refs.editor.quill;
      console.log(desc)
      var selection = desc.getSelection(true);
      console.log(selection,"selection");
      this.$refs.editor.quill.insertEmbed(selection.index, 'code-block','selection');
      console.log("#success#");
      },

   handleClick() { 
     let rawObject = {
       'blog_title':this.blog_title,
       'blog_description': this.blog_description,
     }
    rawObject = JSON.stringify(rawObject)
    let formData = new FormData()
    console.log(formData,"before apend")

    formData.append('blog_title',this.blog_title)
    formData.append('blog_description',this.blog_description)
    formData.append('blog_image',this.blog_image)
    formData.append('keywords',key_arr)


    for (var key of formData.entries()) {
        console.log(key[0] + ', ' + key[1]);
    }

    this.$http.post("http://localhost:4000/api/blog/create",formData,{
        headers: {
          'Accept': 'application/json',
          'Content-Type':'multipart/form-data'
            }
        })
      .then(function(data){
        console.log(data.data)
        this.$router.push({path:'/'+data.data.slug}); 
      })
   
    //  this.$router.push({ name: 'blog', params:{'slug':text} })
         },
    onEditorBlur(editor) {
      console.log("editor blur!", editor);
    },

    onUpload(e){
     var files = e.target.files || e.dataTransfer.files;
     if (!files.length)
    return;
    this.blog_image = files[0]
    this.blog_image_url = URL.createObjectURL(files[0]);
    console.log(this.blog_image_url)
    console.log(this.blog_image,'image')
     },

    addtext() {
   
      console.log("button clicked");
      const desc = this.$refs.editor.quill;
      console.log(desc)

      var selection = desc.getSelection(true);
      console.log(selection,"selection");

      this.$refs.editor.quill.insertText(selection.index, 'MASTROLINKS');
      // this.$refs.editor.quill.insertEmbed(length, 'image', res.url);
      console.log("#success#");
    },

    inputChangeImg(){    
      console.log('function called')
      var file = document.querySelector('#selectImg').files[0];
      console.log('file',file)
      var reader = new FileReader();
      let src = ""

      reader.addEventListener("load", () => {
        const src = reader.result; 
        this.img_src = src
        let quill = this.$refs.editor.quill
      let length = quill.getSelection(true).index;
      quill.insertEmbed(length, 'image', src);
        // imageTag = `<img src="${src}">` ;
        // console.log(imageTag);          
        }, false);  

      if (file) {
        reader.readAsDataURL(file);
      }  
        // console.log("reader.result(src222)",  this.img_src)


      
      // this.$refs.editor.quill.insertText(selection.index, imageTag);
      console.log("#success#");


    }
  } 

};


</script>

<style>
.width100 {
  width: 100%;
}
.dashboard li {
  list-style: none;
  display: inline-block;
  font-size: 12px;
}
.Blog-content {
  padding: 20px;
}

.img-first {
  height: 20px;
}
.button-box {
  border: 1px solid #007bff;
  border-radius: 3px;
  display: flex;
  justify-content: center;
  padding: 16px;
}
#main_photo{
  font-size:25px;
  color:grey;
  border:none;
  position: absolute;

}
.btn.btn-primary {
  font-size: 12px;
}
.icon-bar a {
  float: left;
  width: 20%;
  text-align: center;
  padding: 12px 0;
  transition: all 0.3s ease;
  color: black;
  font-size: 20px;
}
.in-field {
  width: 100%;
  padding: 3px 30px;
  font-size: 30px;
  background: #f2f2f2;
  font-weight: 600;
  border: none;
}
.img-text {
  font-family: fantasy;
  padding: 10px 12px 0px;
  font-size: larger;
  color: gray;
}
.child_label {
  box-sizing: border-box;
  font-family: Helvetica, Arial, sans-serif;
  font-size: 13px;
  height: 100%;
  margin: 0px;
  position: relative;
  box-sizing: border-box;
  line-height: 1.42;
  height: 100%;
  outline: none;
  border: ridge;
  padding: 12px 15px;
  width: 100%;
  background: #f2f2f2;
}
.add-field {
  position: relative;
}
.text-label {
  font-size: 14px;
  padding-top: 8px;
}
.form-control {
  font-size: 11px;
  height: 36px;
}
.add-outer {
  width: 26px;
  height: 26px;
  background-color: #007bff;
  border-radius: 2px;
  color: #fff;
  justify-content: center;
  display: flex;
  align-items: center;
  position: absolute;
  right: 4px;
  top: 42px;
}


.fas.fa-plus-square {
  font-size: 30px;
}
.bg-grey {
  background: url("https://static-exp1.licdn.com/sc/h/9umi21lvbdkhlz1fzfto0ks1p")
    center center no-repeat #e4e4e4;
  height: 200px;
}
.image__class img{
  height: 200px;
}
#file {
  opacity: 0;
  height: 200px;
  width: 100%;
}
.editor-container {
  position: relative;
  padding-left: 20px;
}
.ql-container {
  position: absolute !important;
  top: 100%;
  left: 7%;
  max-height: 100%;
  width: 93% !important;
  border-top: 1px solid #ccc !important;
}
.add_item{
  width:100%;
  margin-bottom: 15px;
  display: none;
}
.block_items{
  width:95%;
  margin-left: 45px;
  display: inline-block;
}
.all_buttons{
  margin-left:0px;
  width:19%;
  border:none;
}
.pick_content{
  display:none;
  margin-top:12px;
  width:90%;
  height:100px;
  border:1px dashed;
  margin-left:40px
  ;
}
.upload_File{
  padding: 6px 50px;
    margin-top: 34px;
    margin-left: 10%;
}
.submit_Button{
  padding: 7px 15px;
    border: 1px solid;
}

</style>
