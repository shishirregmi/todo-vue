<template>
  <div>
    <!-- <input
        type="text"
        v-model="signupForm.username"
        placeholder="Enter Your UserName"
      /><br /><br />
      <input
        type="password"
        v-model="signupForm.password"
        placeholder="Enter Your Password"
      /><br /><br />
      <p>Hobbies</p>
      <input
        type="checkbox"
        v-model="signupForm.hobbies"
        value="travel"
        id="travel"
      />
      <label for="travel">Travel</label><br /><br />
      <input
        type="checkbox"
        v-model="signupForm.hobbies"
        value="sports"
        id="sports"
      />
      <label for="sports">Sports</label><br /><br />
      <p>Gender</p>
      <input type="radio" v-model="signupForm.gender" value="male" id="male" />
      <label for="male">Male</label><br /><br />
      <input
        type="radio"
        v-model="signupForm.gender"
        value="female"
        id="female"
      />
      <label for="female">Female</label><br /><br /> -->
    <!-- <button v-on:click="signupUser">Sign Up</button> -->
    <p v-if="error.length">
      <b> Please Enter the Username and Password Correctly. </b>
      <ul>
          <p v-for="e in error" v-bind:key="e.id">
              {{e}}
          </p>
      </ul>
    </p>
    <form @submit="signup">
      <input
        type="text"
        placeholder="Enter Username"
        v-model="username"
      /><br /><br />
      <input
        type="password"
        placeholder="Enter Password"
        v-model="password"
      /><br /><br />
      <button type="submit">Sign Up</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "SignUp",
  data() {
    return {
      error: [],
      username: null,
      password: null,
      //   signupForm: {
      //     username: null,
      //     password: null,
      //     hobbies: [],
      //     gender: null,
      //   },
    };
  },
  methods: {
    // signupUser() {
    //   console.log(this.signupForm);
    // },

    signup(e) {
      if (this.name && this.password) {
        console.warn("Signned Up");
      }
      this.error = [];
      if (!this.username) {
        this.error.push("Username is required");
      }
      if (!this.password) {
        this.error.push("Password is required");
      }
      console.warn("errors", this.error);
      e.preventDefault();
    },
  },
};
</script>