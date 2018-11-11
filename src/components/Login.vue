<template>
  <div id="login">
    <button @click="loginGoogle">Login Google Account</button>
  </div>
</template>

<script>
export default {
  name: "login",
  data() {
    return {
      
    }
  },
  methods: {
    loginGoogle() {
      firebase.auth().signInWithRedirect(new firebase.auth.GoogleAuthProvider())
    }
  }
}
</script>