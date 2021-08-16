<template>
  <div class="home">
    <h1>Home Component</h1>
    <Users />
    <Products />
  </div>
</template>

<script>
import Users from "./Users";
import Products from "./Products";

export default {
  name: "HomeView",
  components: {
    Users,
    Products,
  },
};
</script>

<style scoped>
.home {
  background-color: aquamarine;
  height: 500px;
}
</style>
