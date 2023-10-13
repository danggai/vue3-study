
<template>
  <form id="123" action="" @submit.prevent="submitForm">
    <div>
      <label for="userId">ID: </label>
      <input id="userid" type="text" v-model="username">
    </div>
    <div>
      <label for="password">PW: </label>
      <input id="password" type="text" v-model="password">
    </div>
    <button type="submit"> 로그인 </button>
  </form>
</template>

<script>
import axios from 'axios'
import { ref } from 'vue';

export default {
  setup() {
    const username = ref('')
    const password = ref('')

    const submitForm = () => {
      axios.post('https://jsonplaceholder.typicode.com/users/', {
        username: username.value,
        password: password.value
      }).then(response => {
        console.log(response);
      }) 
    }

    return { username, password, submitForm }
  }
  
  // data() {
  //   return { 
  //     username: "",
  //     password: ""
  //   }
  // },
  // methods: {
  //   submitForm() {
  //     const data = {
  //       username: this.username,
  //       password: this.password
  //     }

  //     axios.post('https://jsonplaceholder.typicode.com/users/', data)
  //     .then(response => {
  //       console.log(response)
  //     });
  //     console.log("제출 됨")
  //   }
  // },
}
</script>

<style scoped>

</style>