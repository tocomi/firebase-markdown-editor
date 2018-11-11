<template>
  <div id="editor">
    <h1>Markdown Editor</h1>
    <h3>{{ user.displayName }}</h3>
    <button @click="logout">Logout</button>
  </div>
</template>

<script>
export default {
  name: "editor",
  props: [ "user" ],
  data() {
    return {
      
    }
  },
  methods: {
    logout() {
      firebase.auth().signOut()
    }
  }
}
</script>
