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
              placeholder="Add todo"
              v-model="name"
              @keyup.enter="addTask"
            />
            <button id="checkAll" class="btn btn-success">
              Mark all as done
            </button>

            <hr />
            <ul id="list-items" class="list-unstyled">
              <li class="ui-state-default" v-for="task of tasks" :key="task.id">
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
              </li>
            </ul>
          </div>
        </div>
        <div class="col-md-6">
          <div class="todolist">
            <h1>Already Done</h1>
            <ul id="done-items" class="list-unstyled">
              <li v-for="task of tasks" :key="task.id">
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
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",

  data() {
    return {
      tasks: [],
      name: "",
    };
  },

  methods: {
    async addTask() {
      const result = await axios.post("http://localhost:3000/tasks", {
        name: this.name,
      });

      this.tasks = [...this.tasks, result.data];
      this.name = "";
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

  async created() {
    try {
      const result = await axios.get("http://localhost:3000/tasks");
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
.form-control {
  border-radius: 0;
}
li.ui-state-default {
  background: #fff;
  border: none;
  border-bottom: 1px solid #ddd;
}

li.ui-state-default:last-child {
  border-bottom: none;
}

.todo-footer {
  background-color: #f4fce8;
  margin: 0 -20px -10px -20px;
  padding: 10px 20px;
}
#done-items li {
  padding: 10px 0;
  border-bottom: 1px solid #ddd;
  text-decoration: line-through;
}
#done-items li:last-child {
  border-bottom: none;
}
#list-items li {
  padding: 10px 0;
  border-bottom: 1px solid #ddd;
}
#list-items li:last-child {
  border-bottom: none;
}
#checkAll {
  margin-top: 10px;
}
</style>
