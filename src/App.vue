<template>
  <SignUpView/>
</template>

<script>
import SignUpView from './views/signUp/SignUpView.vue';

export default {
  name: 'App',
  components: {
    SignUpView
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
