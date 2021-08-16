<template>
  <div>
    <h1>Student</h1>
    <h3>Current Student Id: {{ this.studentId }}</h3>
  </div>
</template>

<script>
export default {
  name: "Student",
  data() {
    return {
      studentId: this.$route.params.id,
    };
  },
};
</script>