<template>
  <div id="editor">
    <h1>Markdown Editor</h1>
    <span>{{ user.displayName }}</span>
    <button @click="logout">Logout</button>
    <div class="editorWrapper">
      <textarea class="markdown" v-model="markdown"></textarea>
      <div class="preview" v-html="preview()"></div>
    </div>
  </div>
</template>

<script>
import marked from "marked"
export default {
  name: "editor",
  props: [ "user" ],
  data() {
    return {
      markdown: "",
    }
  },
  methods: {
    logout() {
      firebase.auth().signOut()
    },
    preview() {
      return marked(this.markdown)
    }
  }
}
</script>

<style scoped>
.editorWrapper {
  display: flex;
}
.markdown {
  width: 50%;
  height: 500px;
}
.preview {
  width: 50%;
  text-align: left;
}
</style>

