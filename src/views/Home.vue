<template>
  <div class="home">
    <h2>Todo: Django & Vue</h2>
    <hr />
    <TodoInput @createTodoEvent="createTodo" />
    <TodoList :todos="todos" />
  </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";
import TodoInput from "@/components/TodoInput.vue";
import router from "@/router";
import jwtDecode from "jwt-decode";
import axios from "axios";

// @ is an alias to /src
// import  from '@/components/'

export default {
  name: "home",
  data() {
    return {
      todos: []
    };
  },
  components: {
    TodoList,
    TodoInput
  },
  methods: {
    loggedIn() {
      this.$session.start();
      if (!this.$session.has("jwt")) {
        router.push("/login");
      }
    },
    getTodos() {
      const token = this.$session.get("jwt");
      const user_id = jwtDecode(token).user_id;
      const options = {
        headers: {
          Authorization: "JWT " + token
        }
      };
      // axios --> api/v1/users/<접속유저 id>
      axios
        .get(`http://localhost:8000/api/v1/users/${user_id}/`, options)
        .then(res => {
          this.todos = res.data.todo_set;
          // console.log(res.data)
        });
    },
    createTodo(title) {
      const token = this.$session.get("jwt");
      const user_id = jwtDecode(token).user_id;
      const options = {
        headers: {
          Authorization: "JWT " + token
        }
      };
      const data = new FormData();
      // data.append(inputName, inputValue)
      data.append('user', user_id);
      data.append('title', title)
      axios.post("http://localhost:8000/api/v1/todos/", data, options)
      .then(res => {
        this.todos.push(res.data)
      })
    }
    
  },
  mounted() {
    this.loggedIn();
    this.getTodos();
  }
};
</script>
