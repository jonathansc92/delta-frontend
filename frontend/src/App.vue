<template>
  <div class="container">
    <StudentsForm title="Cadastrar Estudante"/>
  </div>
</template>

<script>
import StudentsForm from './components/StudentsForm.vue'

export default {
  name: 'App',
  components: {
    StudentsForm
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
