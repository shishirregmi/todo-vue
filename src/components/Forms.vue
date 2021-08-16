<template>
  <div>
    <h1>Form</h1>
    <input
      type="text"
      v-model="loginForm.username"
      placeholder="Enter Username"
    /><br /><br />
    <input
      type="password"
      v-model="loginForm.password"
      placeholder="Enter Password"
    /><br /><br />
    <button v-on:click="getLogin">Login</button>
  </div>
</template>
<script>
export default {
  name: "Forms",
  data() {
    return {
      loginForm: {
        username: null,
        password: null,
      },
    };
  },
  methods: {
    getLogin() {
      console.log(this.loginForm);
    },
  },
};
</script>