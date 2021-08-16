<template>
  <div>
    <form @submit="postData" method="post">
      <input
        type="text"
        placeholder="Enter Title"
        name="title"
        v-model="posts.title"
        id="name"
      /><br /><br />
      <input
        type="text"
        placeholder="Enter Author Name"
        name="author"
        v-model="posts.author"
        id="author"
      /><br /><br />
      <button type="Submit">Submit</button>
    </form>
    <table border="1">
      <tr>
        <th>ID</th>
        <th>Title</th>
        <th>Author</th>
        <th>Action</th>
      </tr>
      <tr v-for="post in getPosts" v-bind:key="post.id">
        <td>{{ post.id }}</td>
        <td>{{ post.title }}</td>
        <td>{{ post.author }}</td>
        <td><button v-on:click="deletePost(post.id)">Delete</button></td>
      </tr>
    </table>
  </div>
</template>
<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
Vue.use(VueAxios, axios);
export default {
  name: "PostComponent",
  data() {
    return {
      posts: {
        id: null,
        title: null,
        author: null,
      },
      getPosts: null,
    };
  },
  methods: {
    postData(e) {
      this.axios.post("http://localhost:3000/posts", this.posts).then(() => {
        this.getData();
        this.posts.title = null;
        this.posts.author = null;
      });
      e.preventDefault();
    },
    getData() {
      this.axios.get("http://localhost:3000/posts").then((result) => {
        this.getPosts = result.data;
      });
    },
    deletePost(id) {
      this.axios.delete("http://localhost:3000/posts/" + id).then(() => {
        this.getData();
      });
    },
  },
  mounted() {
    this.getData();
  },
};
</script>