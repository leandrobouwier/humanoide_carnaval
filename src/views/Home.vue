<template>
  <div>
    <section>
      <div class="banner">
        <div class="conteudo-banner">
          <h2>
            Ainda dá tempo de
            <b>ser felix</b>
          </h2>
          <p>
            Fantasias premiun por
            <span>$100,00</span>
          </p>
          <button class="button-home" @click="scrollBottom">Comprar Agora</button>
        </div>
        <img src="../assets/images/banner.jpg">
      </div>
    </section>
  </div>
</template>

<script>
export default {
  methods: {
    scrollBottom() {
      window.scrollTo({
        top: 600,
        behavior: "smooth"
      });
    }
  }
};
</script>

<style scoped>
@import "../assets/css/home.css";
</style>
