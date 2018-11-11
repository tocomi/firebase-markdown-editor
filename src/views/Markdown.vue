<template>
  <div class="markdown">
    <Editor v-if="isLogin" :user="userData"></Editor>
    <Login v-if="!isLogin"></Login>
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
    }
  },
  created() {
    firebase.auth().onAuthStateChanged(user => {
      console.log(user)
      if (user) {
        this.isLogin = true
        this.userData = user
      } else {
        this.isLogin = false
        this.userData = null
      }
    })
  },
  components: {
    Login: Login,
    Editor: Editor,
  }
}
</script>
