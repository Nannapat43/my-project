<template>
    <Welcome />
  </template>
  
  <script>
  import { defineComponent } from 'vue';
  
  // Components
  import Welcome from '../components/Welcome.vue';
  
  export default defineComponent({
    name: 'WelcomeView',
  
    components: {
        Welcome,
    },
  });
  </script>
  