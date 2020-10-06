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
          <section class>
            <quill-editor
              ref="editor"
              @blur="onEditorBlur($event)"
              @focus="onEditorFocus($event)"
              @ready="onEditorReady($event)"
            />

            <div class="bg-grey">
              <input id="file" type="file" />
            </div>
            <client-only>
              <div ref="editor" class="ql-editor" contenteditable></div>
            </client-only>
            <input field class="in-field" placeholder="HeadLine" />
            <br />
            <br />
            <span>
              <img
                class="img-first"
                src="https://img.icons8.com/ios/452/add-book.png"
              />
              <span class="img-text"
                >Write here.Add video or images for visual impact</span
              >
            </span>
          </section>
        </div>
        <div class="col-sm-3">
          <div class="button-box">
            <b-button variant="primary">Save and Publish</b-button>
          </div>
          <div class="add-field">
            <div>
              <label class="text-label">Tags</label>
              <b-form-input
                v-model="text"
                placeholder="Add Keywords"
              ></b-form-input>
              <div class="add-outer">+</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "quill-example-nuxt",
  data() {
    return {
      editorOption: {
        // Some Quill options...
        theme: "snow",
        modules: {
          toolbar: [
            ["bold", "italic", "underline", "strike"],
            [{ list: "ordered" }, { list: "bullet" }],
            [{ header: [1, 2, 3, 4, 5, 6, false] }],
            [{ color: [] }, { background: [] }],
            [{ font: [] }],
            [{ align: [] }],
            ["link", "image"],
            ["clean"]
          ]
        }
      }
    };
  },
  mounted() {
    // console.log(
    //   "App inited, the Quill instance object is:",
    //   this.$refs.editor.quill
    // );
    console.log(this.$refs["editor"].quill.addContainer("ql-xtz"));
  },
  methods: {
    onEditorBlur(editor) {
      console.log("editor blur!", editor);
    },
    onEditorFocus(editor) {
      console.log("editor focus!", editor);
    },
    onEditorReady(editor) {
      console.log("editor ready!", editor);
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
.ql-editor {
  display: none;
}

.fas.fa-plus-square {
  font-size: 30px;
}
.bg-grey {
  background: url("https://static-exp1.licdn.com/sc/h/9umi21lvbdkhlz1fzfto0ks1p")
    center center no-repeat #e4e4e4;
  height: 200px;
}
#file {
  opacity: 0;
  height: 200px;
  width: 100%;
}
</style>
