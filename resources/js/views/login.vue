<template>
  <div class="main">
    <h4>Login</h4>
    <form @submit.prevent="login">

      <label for="email" >E-Mail Address</label>
      <div>
          <input id="email" type="email" v-model="email" required>
      </div>

      <label for="password">Password</label>
      <div>
          <input id="password" type="password" v-model="password" required>
      </div>

      <!-- <label for="password-confirm">Confirm Password</label> -->
      <!-- <div> -->
          <!-- <input id="password-confirm" type="password" v-model="password_confirmation" required> -->
      <!-- </div> -->

      <div>
          <button type="submit" class="btn-primary">Login</button> <br> 
          Dont have an account ?  <router-link :to="{ name: 'register' }">Register</router-link> here.
      </div>
    </form>
  </div>
</template>

<script>
import axios from 'axios';
    export default {
        data() {
    return {
      
      email: '',
      password: ''
    }
  },


 methods: {
            login() {
                     const { email, password } = this
      const data = {  email, password }
      const URL = '/api/login'
      axios({
        method: 'post',
        url: URL,
        headers: {
          Accept: 'application/json',
          Content: 'application/json'
        },
        data: data
      })
        .then(res => {
          sessionStorage.setItem('token', res.data.success.token)
          this.$router.push('/dashboard')
        })
        .catch(err => {

          // eslint-disable-next-line
           alert('Wrong email/password')
          // eslint-disable-next-line
          console.log(err.data)
        })
    }
}
}


       
</script>