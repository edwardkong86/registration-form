<template>
  <div id="app">
    <RegistrationForm />
  </div>
</template>

<script>
import RegistrationForm from './components/RegistrationForm.vue';

export default {
  name: 'App',
  components: {
    RegistrationForm,
  },
};
</script>

<style>
/* You can add global styles here */
/* Global font family set to Arial */
html, body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}
</style>