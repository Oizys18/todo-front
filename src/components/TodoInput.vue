<template>
  <div class="todo-input">
    <h2>Todo Input</h2>
    <div >
      <form @submit.prevent="createTodo" class="input-group mb-3">
        <input v-model="title" type="text" class="form-control"/>
        <button type="submit" class="btn btn-primary">+</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoInput",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    createTodo() {
      this.$emit("createTodoEvent", this.title);
      this.title = "";
    }
  }
};
</script>

<style>
</style>