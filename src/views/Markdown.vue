<template>
  <div class="markdown">
    <Editor v-if="isLogin" :user="userData"></Editor>
    <Login v-if="!isLogin && !nowLoading"></Login>
    <span v-if="nowLoading">Now Loading...</span>
  </div>
</template>

<script>
import Login from "@/components/Login.vue"
import Editor from "@/components/Editor.vue"

export default {
  name: "markdown",
  data() {
    return {
      isLogin: false,
      userData: null,
      nowLoading: false,
    }
  },
  created() {
    this.nowLoading = true
    firebase.auth().onAuthStateChanged(user => {
      if (user) {
        this.isLogin = true
        this.userData = user
      } else {
        this.isLogin = false
        this.userData = null
      }
      this.nowLoading = false
    })
  },
  components: {
    Login: Login,
    Editor: Editor,
  }
}
</script>
