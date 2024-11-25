<template>
    <button class="app-button" @click="$emit('click')">
      <slot />
    </button>
  </template>
  
  <script lang="ts">
  export default {};
  </script>
  
  <style scoped>
  .app-button {
    padding: 10px 20px;
    border: none;
    background-color: #3498db;
    color: white;
    font-size: 16px;
    border-radius: 4px;
    cursor: pointer;
  }
  </style>