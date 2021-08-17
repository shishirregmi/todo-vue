<template>
  <div>
    <input
      type="text"
      class="form-control add-todo"
      placeholder="Add task"
      v-model="name"
      @keyup.enter="addTask"
    />
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "AddNew",
  props: ["tasks"],
  data() {
    return {
      name: "",
    };
  },
  methods: {
    async addTask() {
      await axios
        .post("http://localhost:3000/tasks/", {
          name: this.name,
          status: false,
        })
        .then((result) => {
          this.$emit("updateTasks", [...this.tasks, result.data]);
          this.name = "";
        });
    },
  },
};
</script>