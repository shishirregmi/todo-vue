<template>
  <div>
    <h1>Bind Component</h1>
    <textarea type="text" v-model="message" />
    <h2 style="white-space: pre-line">{{ message }}</h2>
  </div>
</template>

<script>
export default {
  name: "DataBinding",
  data() {
    return {
      message: "",
    };
  },
};
</script>
