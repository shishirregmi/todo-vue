<template>
  <div>
    <button v-on:click="updateTitle">Update Title</button>
  </div>
</template>

<script>
export default {
  name: "Child",
  methods: {
    updateTitle() {
      this.$emit("changeTitle", "Form Child");
    },
  },
};
</script>
