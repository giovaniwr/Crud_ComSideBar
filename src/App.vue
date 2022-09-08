<template>
  <NavSide :logo="logo_src" alt_src="app_name" />
  <router-view />
  <Footer />
</template>


<script>
import NavSide from './components/NavSide.vue';
import Footer from './components/Footer.vue';
  export default{
    components: {
      NavSide,
      Footer
    },
    data() {
      return {
        logo_src: "/img/logo.png",
        app_name: "Logo do Banco"
    }
  }
}
</script>

<style>
  *{
    font-family: helvetica;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container {
    margin: 50px;
    min-height: 100px;
  }
  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }

</style>
