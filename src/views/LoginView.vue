<template>
  <div class="container">
    <input type="checkbox" id="register_toggle" v-model="isRegister" aria-hidden="true" />

    <div class="slider">
      <!-- Login Form -->
      <form @submit.prevent="submitLogin" class="form">
        <h2 class="title">Login</h2>
        <div class="form_control">
          <input type="email" v-model="login.email" required class="input" />
          <label for="email" class="label">Email</label>
        </div>
        <div class="form_control">
          <input type="password" v-model="login.password" required class="input" />
          <label for="password" class="label">Password</label>
        </div>
        <button type="submit">Login</button>
        <p class="bottom_text">Don't have an account? <span class="switch" @click="toggleForm">Sign up</span></p>
      </form>

      <!-- Signup Form -->
      <form @submit.prevent="submitSignup" class="form">
        <h2 class="title">Sign Up</h2>
        <div class="form_control">
          <input type="text" v-model="signup.username" required class="input" />
          <label for="username" class="label">Username</label>
        </div>
        <div class="form_control">
          <input type="email" v-model="signup.email" required class="input" />
          <label for="email" class="label">Email</label>
        </div>
        <div class="form_control">
          <input type="password" v-model="signup.password" required class="input" />
          <label for="password" class="label">Password</label>
        </div>
        <button type="submit">Sign Up</button>
        <p class="bottom_text">Already have an account? <span class="switch" @click="toggleForm">Login</span></p>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isRegister: false,
      login: {
        email: '',
        password: ''
      },
      signup: {
        username: '',
        email: '',
        password: ''
      }
    };
  },
  methods: {
    toggleForm() {
      this.isRegister = !this.isRegister;
    },
    submitLogin() {
      console.log('Login submitted:', this.login);
    },
    submitSignup() {
      console.log('Signup submitted:', this.signup);
    }
  }
};
</script>

<style scoped>
.container {
  margin-top: 150px !important;
  width: 300px;
  margin: auto;
  padding: 20px;
  border-radius: 5px;
  overflow: hidden;
  color: white;
  box-shadow: 1.5px 1.5px 3px #0e0e0e, -1.5px -1.5px 3px rgb(95 94 94 / 25%), inset 0px 0px 0px #0e0e0e, inset 0px -0px 0px #5f5e5e;
  background-color: #333;
}

.container .slider {
  width: 200%;
  position: relative;
  transition: transform ease-out 0.3s;
  display: flex;
}

#register_toggle {
  display: none;
}

.container #register_toggle:checked + .slider {
  transform: translateX(-50%);
}

.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 20px;
  padding: 1.5em 3em;
  width: 50%;
}

.title {
  text-align: center;
  font-weight: 700;
  font-size: 1.5em;
}

.form_control {
  width: 100%;
  position: relative;
  overflow: hidden;
}

.label {
  position: absolute;
  top: 50%;
  left: 10px;
  transition: transform ease 0.2s;
  transform: translate(0%, -50%);
  font-size: 0.75em;
  user-select: none;
  pointer-events: none;
  color: #b0b0b0;
}

.input {
  width: 100%;
  background-color: #444;
  border: 1px solid #ccc;
  outline: none;
  color: #fff;
  padding: 10px;
  font-size: 1em;
  border-radius: 5px;
  transition: box-shadow ease 0.2s;
}

.input:focus,
.input:valid {
  box-shadow: inset 0 0 5px #0e0e0e;
}

.input:focus + .label,
.input:valid + .label {
  transform: translate(-150%, -50%);
}

button {
  width: 100%;
  background-color: #444;
  border: 1px solid #ccc;
  outline: none;
  color: #fff;
  padding: 10px;
  font-size: 1em;
  border-radius: 5px;
  cursor: pointer;
  transition: box-shadow ease 0.1s;
}

button:active {
  box-shadow: inset 0 0 5px #0e0e0e;
}

.bottom_text {
  font-size: 0.85em;
}

.switch {
  font-weight: 700;
  cursor: pointer;
  color: #007BFF;
}
</style>
