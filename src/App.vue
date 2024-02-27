<template>
  <div class="form-container">
    <p class="success" v-if="isSubmitted">Success! Thank you for registering</p>
    <form @submit.prevent="onSubmit">
      <input
        autocomplete="off"
        class="form-field"
        type="text"
        name="firstname"
        placeholder="First name"
        v-model="firstName.value"
        @blur="validateRequired('firstName')"
      />
      <small class="error" v-if="!firstName.valid">*First name is required</small>
      <input
        autocomplete="off"
        class="form-field"
        type="text"
        name="lastname"
        placeholder="Last name"
        v-model="lastName.value"
        @blur="validateRequired('lastName')"
      />
      <small class="error" v-if="!lastName.valid">*Last name is required</small>
      <input
        autocomplete="off"
        class="form-field"
        type="email"
        name="email"
        placeholder="Email"
        v-model="email.value"
        @blur="validateRequired('email')"
      />
      <small class="error" v-if="!email.valid">*Email is invalid</small>
      <button class="form-field">register</button>
    </form>
  </div>
</template>

<script lang="ts">
  export default {
    data() {
      return {
        isSubmitted: false,
        firstName: {
          value: "",
          valid: true
        },
        lastName: {
          value: "",
          valid: true
        },
        email: {
          value: "",
          valid: true
        }
      }
    },
    methods: {
      validateRequired(field: "firstName" | "lastName" | "email") {
        switch (field) {
          case "firstName":
            if (!this.firstName.value.trim()) {
              this.firstName.valid = false
            } else {
              this.firstName.valid = true
            }
            return this.firstName.valid
          case "lastName":
            if (!this.lastName.value.trim()) {
              this.lastName.valid = false
            } else {
              this.lastName.valid = true
            }
            return this.lastName.valid
          case "email":
            if (!this.email.value.trim()) {
              this.email.valid = false
            } else {
              this.email.valid = true
            }
            return this.email.valid
        }
      },
      resetFields() {
        this.firstName = {
          value: "",
          valid: true
        }
        this.lastName = {
          value: "",
          valid: true
        }
        this.email = {
          value: "",
          valid: true
        }
      },
      onSubmit() {
        if (this.validateRequired("firstName") 
          && this.validateRequired("lastName") 
          && this.validateRequired("email")
        ) {
          this.resetFields()
          this.isSubmitted = true
        }
      }
    }
  }
</script>

<style>
  body {
    background-color: #76b852;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    font-family: Arial, Helvetica, sans-serif;
  }

  .form-container {
    width: 360px;
    background-color: white;
    margin: auto;
    padding: 10px;
    box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2), 0 5px 5px 0 rgba(0, 0, 0, 0.24);
    border-radius: 6px;
  }

  form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 10px;
  }

  .success {
    background-color: #3f89f8;
    padding: 15px;
    color: white;
    border-radius: 6px;
  }

  .form-field {
    margin: 10px 0;
    padding: 15px;
    font-size: 16px;
    border: 0;
    border-radius: 6px;
  }

  input {
    background: #f2f2f2;
  }

  button {
    background-color: #4caf50;
    color: white;
    cursor: pointer;
  }

  button:hover {
    background-color: #3e6b40;
  }

  span {
    font-size: 14px;
    color: red;
    margin-bottom: 15px;
  }

  .error {
    color: red;
  }
</style>