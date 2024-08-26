<template>
    <header class="header">
      <div class="brand">
        <img src="https://via.placeholder.com/100" alt="Brand Logo" class="logo" />
        <h1 class="brand-name">Jewelry Store</h1>
      </div>
      <div class="button-container">
        <button @click="openForm('buy')">Buy Jewelry</button>
        <button @click="openForm('sell')">Sell Jewelry</button>
      </div>
    </header>
  </template>
  
  <script>
  export default {
    methods: {
      openForm(formType) {
        this.$emit('open-form', formType);
      }
    }
  }
  </script>
  
  <style scoped>
  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    /* padding: 1rem; */
    background-color: #333;
    color: white;
    /* width: 100vw; */

  }
  
  .brand {
    display: flex;
    align-items: center;
  }
  
  .logo {
    width: 50px;
    height: 50px;
    margin-right: 1rem;
  }
  
  .brand-name {
    font-size: 1.5rem;
    margin: 0;
  }
  
  .button-container button {
    background-color: #ac42c0;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    font-size: 1rem;
    cursor: pointer;
    border-radius: 5px;
    margin-left: 0.5rem;
    transition: background-color 0.3s ease;
  }
  
  .button-container button:hover {
    background-color: #6d42c0;
  }
  </style>
  