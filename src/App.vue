<template>
  <div class="container-fluid mt-3">
    <div class="card">
      <div class="card-header">
        <header>
          <h2 class="text-center m-0">NT2 - Trabajo Práctico 2</h2>
        </header>
      </div>

      <div class="card-body">
        <main>
          <Form /> 
        </main>
      </div>
  </div>
  </div>
</template>


<script>
import Form from './components/Form.vue';
export default {

  name: 'App',
  components: {
Form,
  },
};
</script>

<style scoped>
.card-header {
  background-color: green;
  color: white;
}

</style>
