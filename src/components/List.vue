<template>
  <div style="margin-top: 20px">
    <ul class="list-group">
      <li v-for="(todo, index) in todos" :key="index" class="list-group-item">
        <div class="row">
          <div class="col">
            <span v-if="todo.isDone"
              ><del>{{ todo.activity }}</del></span
            >
            <span v-else> {{ todo.activity }} </span>
          </div>
          <div class="col-auto">
            <div class="row gx-2">
              <div class="col">
                <button @click="done(index)" class="btn btn-default">✅</button>
              </div>
              <div class="col">
                <button @click="deleteTODO(index)" class="btn btn-default">
                  ❌
                </button>
              </div>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      default: [],
    },
  },
  methods: {
    deleteTODO(index) {
      this.$emit("deleteTODO", index);
    },
    done(index) {
      this.$emit("doneTODO", index);
    },
  },
};
</script>
