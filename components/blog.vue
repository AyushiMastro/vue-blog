<template>
  <div class="position-relative">
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

            <br />
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
                class="add_keywords"
              ></b-form-input>
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
      blog_image_url:''
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
.quill-editor {
  min-height: 200px;
  max-height: 400px;
  overflow-y: auto;
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
.btn.btn-primary {
  font-size: 12px;
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
.quill-editor {
  min-height: 0;
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
}
.ql-container {
  position: absolute !important;
  top: 100%;
  max-height: 100%;
  width: 100% !important;
  border-top: 1px solid #ccc !important;
}
</style>
