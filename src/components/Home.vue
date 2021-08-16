<template>
  <div>
    <p v-html="text"></p>
    <h1 v-if="show">Hello from IF</h1>
    <h1 v-else>Hello from else</h1>
    <h1>{{ fname }}</h1>
    <h1>{{ msg }}</h1>
    <h1>{{ name }}</h1>
    <h3>{{ show ? "yes" : "no" }}</h3>
    <button v-on:click="message">Hello</button>
    <button v-on:click="display">Toggle</button><br /><br />
    <button v-on:mouseover="hello('item')">Call Hello Function</button>
    <table>
      <tr>
        <th>Id</th>
        <th>Name</th>
        <th>Email</th>
      </tr>
      <tr v-for="user in users" :key="user.id">
        <td>{{ user.id }}</td>
        <td>{{ user.name }}</td>
        <td>{{ user.email }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "Home",
  props: {
    fname: String,
    msg: String,
  },
  data() {
    return {
      name: "Shisihr says hi",
      show: true,
      text: "<h1>This runs from data()</h1>",
      users: [
        { id: "1", name: "peter", email: "peter@gmail.com" },
        { id: "2", name: "sam", email: "sam@gmail.com" },
        { id: "3", name: "tony", email: "peter@gmail.com" },
      ],
    };
  },
  methods: {
    hello(item) {
      console.warn("Hello Function Called " + item);
    },
    display() {
      this.show = !this.show;
    },
    message() {
      this.name = "Shishir Says Bye";
      console.warn("Hello Clicked");
    },
  },
};
</script>
