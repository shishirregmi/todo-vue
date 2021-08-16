<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <div class="todolist not-done">
            <h1>Todos</h1>
            <input
              type="text"
              class="form-control add-todo"
              placeholder="Add task"
              v-model="name"
              @keyup.enter="addTask"
            />
            <hr />
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
        </div>
        <div class="col-md-6">
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
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

const url = "http://localhost:3000/tasks/";

export default {
  name: "App",

  data() {
    return {
      tasks: [],
      name: "",
      status: false,
    };
  },

  methods: {
    async addTask() {
      const result = await axios.post(url, {
        name: this.name,
        status: false,
      });
      this.tasks = [...this.tasks, result.data];
      this.name = "";
    },

    async doneTask(taskId) {
      await axios.patch(url + taskId, { status: true }).then(() => {
        const objIndex = this.tasks.findIndex((obj) => obj.id == taskId);
        this.tasks[objIndex].status = true;
      });
    },

    async undoTask(taskId) {
      await axios.patch(url + taskId, { status: false }).then(() => {
        const objIndex = this.tasks.findIndex((obj) => obj.id == taskId);
        this.tasks[objIndex].status = false;
      });
    },

    async deleteTask(taskId) {
      await axios.delete(url + taskId).then(() => {
        this.tasks.splice(
          this.tasks.findIndex(function (i) {
            return i.id === taskId;
          }),
          1
        );
      });
    },
  },

  async created() {
    try {
      const result = await axios.get(url);
      this.tasks = result.data;
    } catch (e) {
      console.error(e);
    }
  },
};
</script>

<style lang="scss">
@import "~@/assets/scss/vendors/bootstrap-vue/index";
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css");

body {
  background-color: #eeeeee;
}

.todolist {
  background-color: #fff;
  padding: 20px 20px 10px 20px;
  margin-top: 30px;
}
.todolist h1 {
  margin: 0;
  padding-bottom: 20px;
  text-align: center;
}
li.ui-state-default {
  background: #fff;
}

.todo-footer {
  background-color: #f4fce8;
  margin: 0 -20px -10px -20px;
  padding: 10px 20px;
}
#done-items li {
  padding: 10px 0;
  text-decoration: line-through;
}
#list-items li {
  padding: 10px 0;
}
#checkAll {
  margin-top: 10px;
}

.inp {
  outline: 0;
  border-width: 0 0 2px;
  border-color: blue;
}
.inp:focus {
  border-color: green;
}
</style>
