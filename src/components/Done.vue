<template>
  <div class="todolist">
    <h1>Already Done</h1>
    <ul id="done-items" class="list-unstyled">
      <div v-for="task of tasks" :key="task.id">
        <li v-if="task.status">
          {{ task.name }}
          <button
            class="remove-item btn btn-default btn-xs pull-right"
            v-on:click="deleteTask(task.id)"
          >
            <i class="fa fa-trash-o" aria-hidden="true"></i>
          </button>
          <button
            class="remove-item btn btn-default btn-xs pull-right"
            v-on:click="undoTask(task.id)"
          >
            <i class="fa fa-undo" aria-hidden="true"></i>
          </button>
        </li>
      </div>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Done",
  props: ["tasks"],
  methods: {
    async deleteTask(taskId) {
      await axios.delete("http://localhost:3000/tasks/" + taskId).then(() => {
        this.tasks.splice(
          this.tasks.findIndex(function (i) {
            return i.id === taskId;
          }),
          1
        );
      });
    },

    async undoTask(taskId) {
      await axios
        .patch("http://localhost:3000/tasks/" + taskId, { status: false })
        .then(() => {
          const objIndex = this.tasks.findIndex((obj) => obj.id == taskId);
          this.tasks[objIndex].status = false;
        });
    },
  },
};
</script>
