<template>
  <div id="editor">
    <h1>Markdown Editor</h1>
    <span>{{ user.displayName }}</span>
    <button @click="logout">Logout</button>
    <h3 v-if="nowLoading">Now Loading...</h3>
    <div v-if="!nowLoading" class="editorWrapper">
      <textarea class="markdown" v-model="memos[0].markdown"></textarea>
      <div class="preview" v-html="preview()"></div>
    </div>
    <button v-if="!nowLoading" class="saveMemosBtn" @click="saveMemos">Save</button>
  </div>
</template>

<script>
import marked from "marked"
export default {
  name: "editor",
  props: [ "user" ],
  data() {
    return {
      memos: [
        {
          markdown: "",
        }
      ],
      nowLoading: false,
    }
  },
  created() {
    this.nowLoading = true
    firebase.database().ref("memos/" + this.user.uid).once("value").then(result => {
      if (result.val()) {
        this.memos = result.val()
      }
      this.nowLoading = false
    })
  },
  methods: {
    logout() {
      firebase.auth().signOut()
    },
    preview() {
      return marked(this.memos[0].markdown)
    },
    saveMemos() {
      firebase.database().ref("memos/" + this.user.uid).set(this.memos)
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

