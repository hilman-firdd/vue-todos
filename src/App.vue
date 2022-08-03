<template>
  <div class="container" style="margin-top: 20px">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">SIMPLE TODO APP</h5>
        <div class="row">
          <div class="col-10">
            <input
              type="text"
              v-model="todo"
              class="form-control"
              @keyup.enter="add"
            />
          </div>
          <div class="col-2">
            <button class="btn btn-success" @click="add">ADD</button>
          </div>
        </div>
        <list :todos="todos" @deleteTODO="deleteTodo" @doneTODO="doneTodo" />
        <br />
        <small>Total TODO : {{ totalTODO }}</small>
      </div>
    </div>
  </div>
</template>

<script>
import list from "./components/List.vue";
export default {
  components: {
    list,
  },
  data() {
    return {
      todo: "",
      todos: [],
    };
  },
  computed: {
    totalTODO() {
      return this.todos.length;
    },
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos"));
  },
  methods: {
    add() {
      //data terbaru unshift
      // this.todos.unshift(this.todo);
      this.todos.unshift({
        activity: this.todo,
        isDone: false,
      });
      this.todo = "";
      this.saveToLocalStorage();
    },
    deleteTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index != todoIndex) {
          return item;
        }
      });
      this.saveToLocalStorage();
    },
    doneTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index == todoIndex) {
          item.isDone = true;
        }

        return item;
      });
      this.saveToLocalStorage();
    },
    saveToLocalStorage() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>
