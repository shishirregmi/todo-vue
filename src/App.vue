<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <div class="todolist not-done">
            <h1>Todos</h1>
            <AddNew
              v-bind:tasks="tasks"
              v-on:updateTasks="updateTasks($event)"
            />
            <hr />
            <NotDone v-bind:tasks="tasks" />
          </div>
        </div>
        <div class="col-md-6">
          <Done v-bind:tasks="tasks" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import AddNew from "./components/AddNew";
import NotDone from "./components/NotDone";
import Done from "./components/Done.vue";

const url = "http://localhost:3000/tasks/";

export default {
  components: { AddNew, NotDone, Done },
  name: "App",

  data() {
    return {
      tasks: [],
      name: "",
      status: false,
    };
  },

  methods: {
    updateTasks(data) {
      this.tasks = data;
    },
  },

  async mounted() {
    await axios.get(url).then((result) => {
      this.tasks = result.data;
    });
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
