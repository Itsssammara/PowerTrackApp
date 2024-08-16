<template>
    <div class="container-form">
      <h6>Contact us for any problems that occur</h6>
      <form @submit.prevent="submitForm">
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="form.name" required />
        
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="form.email" required />
        
        <label for="message">Message:</label>
        <textarea id="message" v-model="form.message" rows="4" required></textarea>
        
        <button type="submit">Send</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        form: {
          name: '',
          email: '',
          message: '',
        },
      };
    },
    methods: {
      submitForm() {
        // Handle form submission
        console.log('Form submitted:', this.form);
      },
    },
  };
  </script>
  
  <style scoped>
.container-form {
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

  
  h6 {
    text-align: center;
    font-size: 1.2rem;
    margin-bottom: 20px;
    color: #333;
  }
  
  form {
    display: flex;
    flex-direction: column;
  }
  
  label {
    margin-bottom: 5px;
    font-weight: bold;
    color: #555;
  }
  
  input[type="text"],
  input[type="email"],
  textarea {
    margin-bottom: 15px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 1rem;
    color: #333;
    transition: border-color 0.3s;
  }
  
  input[type="text"]:focus,
  input[type="email"]:focus,
  textarea:focus {
    border-color: #007bff;
    outline: none;
  }
  
  textarea {
    resize: vertical;
  }
  
  button {
    padding: 10px 15px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  </style>
  