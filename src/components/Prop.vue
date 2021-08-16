<template>
  <div>
    <h1>Child Component</h1>
    <div v-for="user in users" :key="user.name">
      <p>Name: {{ user.name }}</p>
      <p>Email: {{ user.email }}</p>
      <hr />
    </div>
  </div>
</template>

<script>
export default {
  name: "Prop",
  props: ["users"],
};
</script>