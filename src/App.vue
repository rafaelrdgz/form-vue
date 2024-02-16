<script setup>

import Form from "@/components/Form.vue";
</script>

<template>
  <div class="container">
    <h1 class="title">Formulario para Universidad Tecnologica de <br>La Habana</h1>
    <p class="description">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Culpa cumque debitis dolor</p>
    <Form></Form>
  </div>
</template>

<style scoped>
  .title{
    text-align: center;
    margin-top: 70px;
  }
  .description{
    text-align: center;
    margin-top: 1rem;
    margin-bottom: 2rem;
    font-weight: 400;
  }
  .container {
    width: 100%;
    margin: 3.125rem auto 0 auto;
  }
  @media (min-width: 576px) {
    .container {
      max-width: 540px;
    }
  }
  @media (min-width: 768px) {
    .container {
      max-width: 720px;
    }
  }
</style>
