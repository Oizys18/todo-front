<template>
  <div class="home">
    <h2>Todo: Django & Vue</h2>
    <hr>
    <TodoInput />
    <TodoList :todos="todos" />
  </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";
import TodoInput from "@/components/TodoInput.vue";
// @ is an alias to /src
// import  from '@/components/'

export default {
  name: "home",
  data() {
    return {
      todos:[
        {title:'Django DRF login 구현'},
        {title:'JWT 활용 세션 구현'},
        {title:'Todo 관련 API 구현'},
        {title:'Vuex 활용 Flux 아키텍쳐 적용'},
      ],
    }
  },
  components: {
    TodoList,
    TodoInput
  },
  
};
</script>
