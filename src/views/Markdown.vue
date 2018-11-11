<template>
  <div class="markdown">
    <Editor v-if="isLogin"></Editor>
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
    }
  },
  components: {
    Login: Login,
    Editor: Editor,
  }
}
</script>
