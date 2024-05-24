

<template>
    <div class="form-popup">
      <form @submit.prevent="handleSubmit">
        <label>First Name:</label>
        <input type="text" v-model="form.FirstName" required />
        <label>Last Name:</label>
        <input type="text" v-model="form.LastName" required />
        <label>DOB:</label>
        <input type="date" v-model="form.DOB" required />
        <label>Salary:</label>
        <input type="number" v-model="form.Salary" required />
        <label>Address:</label>
        <input type="text" v-model="form.Address" required />
        <button type="submit">Save</button>
        <button type="button" @click="$emit('close')">Cancel</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      employee: Object,
    },
    data() {
      return {
        form: this.employee ? { ...this.employee } : {
          FirstName: '',
          LastName: '',
          DOB: '',
          Salary: '',
          Address: '',
        },
      };
    },
    methods: {
      handleSubmit() {
        this.$emit('save', this.form);
      },
    },
  };
  </script>
  
  <style scoped>
  .form-popup {
    position: fixed;
    top: 20%;
    left: 50%;
    transform: translate(-50%, -50%);
    padding: 20px;
    border: 1px solid #ccc;
    background-color: white;
    z-index: 1000;
  }
  
  form {
    display: flex;
    flex-direction: column;
  }
  
  label {
    margin-bottom: 5px;
  }
  
  input {
    margin-bottom: 10px;
    padding: 5px;
  }
  </style>
  