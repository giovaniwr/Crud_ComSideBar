<template>
  <div class="main-container">
    <h1>Faça seu cadastro</h1>
    <Formulario />
  </div>
</template>

<script>
  import Formulario from "../components/Formulario.vue";
  export default {
    name: "Home",
    components: {
      Formulario,
    },
  };
</script>
