<template>
  <div class="main">
    <input type="checkbox" id="chk" v-model="isChecked" aria-hidden="true" />

    <div class="login">
      <form @submit.prevent="submitLogin">
        <label for="chk" aria-hidden="true">Login</label>
        <input type="email" name="email" placeholder="Email" v-model="login.email" required />
        <input type="password" name="password" placeholder="Password" v-model="login.password" required />
        <button type="submit">Login</button>
      </form>
    </div>

    <div class="signup" :class="{ 'transform-up': isChecked }">
      <form @submit.prevent="submitSignup">
        <label for="chk" aria-hidden="true">Sign up</label>
        <input type="text" name="username" placeholder="User name" v-model="signup.username" required />
        <input type="email" name="email" placeholder="Email" v-model="signup.email" required />
        <input type="number" name="phone" placeholder="Phone Number" v-model="signup.phone" required />
        <input type="password" name="password" placeholder="Password" v-model="signup.password" required />
        <button type="submit">Sign up</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isChecked: false,
      signup: {
        username: '',
        email: '',
        phone: '',
        password: ''
      },
      login: {
        email: '',
        password: ''
      }
    };
  },
  methods: {
    submitSignup() {
      console.log('Signup form submitted', this.signup);
      // Add your signup logic here
    },
    submitLogin() {
      console.log('Login form submitted', this.login);
      // Add your login logic here
    }
  }
};
</script>

<style scoped>
body {
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  font-family: 'Jost', sans-serif;
  background: linear-gradient(to bottom, #0f0c29, #302b63, #24243e);
}

.main {
  width: 350px;
  height: 500px;
  background: red;
  overflow: hidden;
  background: url("https://doc-08-2c-docs.googleusercontent.com/docs/securesc/68c90smiglihng9534mvqmq1946dmis5/fo0picsp1nhiucmc0l25s29respgpr4j/1631524275000/03522360960922298374/03522360960922298374/1Sx0jhdpEpnNIydS4rnN4kHSJtU1EyWka?e=view&authuser=0&nonce=gcrocepgbb17m&user=03522360960922298374&hash=tfhgbs86ka6divo3llbvp93mg4csvb38") no-repeat center/cover;
  border-radius: 10px;
  box-shadow: 5px 20px 50px #000;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

#chk {
  display: none;
}

.login {
  position: relative;
  width: 100%;
  height: 100%;
}

label {
  color: #18191a;
  font-size: 2.3em;
  justify-content: center;
  display: flex;
  margin: 50px;
  font-weight: bold;
  cursor: pointer;
  transition: .5s ease-in-out;
}

input {
  width: 60%;
  height: 10px;
  background: #e0dede;
  justify-content: center;
  display: flex;
  margin: 20px auto;
  padding: 12px;
  border: none;
  outline: none;
  border-radius: 5px;
}

button {
  width: 60%;
  height: 40px;
  margin: 10px auto;
  justify-content: center;
  display: block;
  color: #fff;
  background: #023b21;
  font-size: 1em;
  font-weight: bold;
  margin-top: 30px;
  outline: none;
  border: none;
  border-radius: 5px;
  transition: .2s ease-in;
  cursor: pointer;
}

button:hover {
  background: #6d44b8;
}

.signup {
  height: 460px;
  background: #eee;
  border-radius: 60% / 10%;
  transform: translateY(-450px);
  transition: .8s ease-in-out;
}

.signup.transform-up {
  transform: translateY(-180px);
}

.signup label {
  color: #573b8a;
  transform: scale(.6);
}

#chk:checked ~ .signup label {
  transform: scale(1);
}

#chk:checked ~ .login label {
  transform: scale(.6);
}
</style>
