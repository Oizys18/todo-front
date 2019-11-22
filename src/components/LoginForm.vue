<template>
  <div>
    <div class="form-group">
      <label for="id">ID</label>
      <input v-model="credentials.username" type="text" id="id" class="form-control" placeholder="아이디를 입력해주세요">  
      
    </div>
    <div class="form-group">
      <label for="password">PW</label>
      <input v-model="credentials.password" type="password" id="password" class="form-control" placeholder="비밀번호를 입력해주세요">  
    </div>
    <button @click="login()" class="btn btn-primary">로그인</button>
    
  </div>
</template>

<script>
import axios from 'axios';
import router from '@/router'; // router/index.js에서 export default router 설정했기 때문에 이렇게만 적어도 알아서 가져온다.
// import session from 'vue-session';

export default {
  name: 'LoginForm',
  data(){
    return {
      credentials: {},
    }
  },
  methods:{
    login () {
      // console.log(this.credentials) 
      axios.post('http://127.0.0.1:8000/api-token-auth/',this.credentials)
      .then(res =>{
        // console.log(res.data.token)
        this.$session.start()
        this.$session.set('jwt', res.data.token)
        router.push('/')
      })
    }
  }
}
</script>

<style>

</style>