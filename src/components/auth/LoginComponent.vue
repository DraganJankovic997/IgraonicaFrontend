<template>
  <div class="d-flex justify-content-center" style="height:100%">
    <div>
      <p></p>
      <div>
        <p></p>
          <h3>Login</h3>
          <p>Email: <input type="text" v-model="korisnik.email"></p>
          <p>Password: <input type="password" v-model="korisnik.password"></p>
          <button class="btn btn-success btn-large" @click="callLogin">Login</button>

      </div>
    </div>
  </div>
</template>

<script>
import authenticationService from '../../services/authentication.service';
export default {
  data: function () {
    return {
      korisnik: {
        email: 'test@gmail.com',
        password: 'password'
      }
    }
  },

  methods: {
    callLogin: function () {
      authenticationService.login(this.korisnik)
      .then((res)=> {
        authenticationService.setToken(res['data']['access_token']);
        authenticationService.setUser(res['data']['user']);
        window.location.href = "/";
      })
      .catch((err)=> {
        this.$toastr.e('Greska prilikom prijave korisnika.', 'Greska');
      })
    }
  }
}


</script>

<style>

</style>