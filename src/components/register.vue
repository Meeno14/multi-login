<template>
  <div class="a">
    <div class="kotak_login">
      <p class="tulisan_login">Silahkan Register</p>
      <br>
      <form style="text-align: center;">
        <label>Username</label>
        <input
          type="text"
          name="username"
          v-model="username"
          class="form_login"
          placeholder="Username atau email .."
        />
        <br>
        <label>Password</label>
        <input
          type="password"
          name="password"
          v-model="password"
          class="form_login"
          placeholder="Password .."
        /><br>

        <div @click="login" class="login">
          <bottom><b>Register</b></bottom>
        </div>
        <a href="/login">Sudah Memiliki Akun</a>
        <br />
        <br />
      </form>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "login",
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    async login() {
      const payload = {
          username: this.username,
          password: this.password,
          role: "siswa"
      };
      const register = await axios.post("http://localhost:3000/users", payload)
      var convertToString = JSON.stringify(register.data);
      sessionStorage.setItem("USER_DATA", convertToString);
      this.$router.push("link")
    },
  },
  mounted() {
    this.getUsers();
  },
};
</script>
<style>
h1 {
  text-align: center;
  /*ketebalan font*/
  font-weight: 300;
}
.tulisan_login {
  text-align: center;
  /*membuat semua huruf menjadi kapital*/
  text-transform: uppercase;
}
.kotak_login {
  width: 350px;
  background: white;
  border-radius: 10px;
  height: 350px;
  /*meletakkan form ke tengah*/
  margin: 80px auto;
  padding: 30px 20px;
}
label {
  font-size: 11pt;
}
.form_login {
  /*membuat lebar form penuh*/
  box-sizing: border-box;
  width: 100%;
  padding: 10px;
  font-size: 11pt;
  margin-bottom: 20px;
}
.login {
  background-image:linear-gradient(to right,#46dec5, rgb(151, 222, 70), #46de4b );
  color: white;
  font-size: 11pt;
  width: 100%;
  border: none;
  border-radius: 3px;
  padding: 10px 20px;
  cursor: pointer;
}
</style>