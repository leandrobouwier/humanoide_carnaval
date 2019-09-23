<template>
  <div id="app">
    <Header></Header>
    <router-view></router-view>
    <Produtos></Produtos>
    <Footer></Footer>
  </div>
</template>
<script>
import Header from "@/components/Header.vue";
import Produtos from "@/components/Produtos.vue";
import Footer from "@/components/Footer.vue";

export default {
  components: {
    Header,
    Produtos,
    Footer
  }
};
</script>

<style scoped>
@import "./assets/css/reset.css";
@import "./assets/css/geral.css";
</style>
