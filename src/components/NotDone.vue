<template>
  <div>
    <ul id="list-items" class="list-unstyled">
      <li class="ui-state-default" v-for="task of tasks" :key="task.id">
        <div v-if="!task.status">
          {{ task.name }}
          <button
            class="remove-item btn btn-default btn-xs pull-right"
            v-on:click="deleteTask(task.id)"
          >
            <i class="fa fa-trash-o" aria-hidden="true"></i>
          </button>
          <button
            class="remove-item btn btn-default btn-xs pull-right"
            v-on:click="doneTask(task.id)"
          >
            <i class="fa fa-check" aria-hidden="true"></i>
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "NotDone",
  props: ["tasks"],

  methods: {
    async doneTask(taskId) {
      await axios
        .patch("http://localhost:3000/tasks/" + taskId, { status: true })
        .then(() => {
          const objIndex = this.tasks.findIndex((obj) => obj.id == taskId);
          this.tasks[objIndex].status = true;
        });
    },

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
  },
};
</script>