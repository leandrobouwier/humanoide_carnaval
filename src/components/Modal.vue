<template>
  <section class="modal">
    <div class="modal_container">
      <div class="modal_dados">
        <img src="../assets/images/confetti.svg" alt="logo-modal">
        <h2 class="title-modal">VIVAAAA!</h2>
        <p class="description">Adicionamos o item no seu carrinho!</p>
        <div class="buttons">
          <button class="button-modal" @click="alterar">Continuar comprando</button>
          <button class="button-modal" @click="alterar">Ir para o carrinho</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  props: ["carrinho"],
  data() {
    return {
      carrinhoComponent: this.carrinho
    };
  },
  methods: {
    alterar() {
      this.carrinhoComponent = false;
      this.$emit("update:carrinho", this.carrinhoComponent);
    }
  }
};
</script>

<style>
.modal {
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal_container {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: absolute;
  top: 0px;
  z-index: 2;
  background: white;
  width: 48%;
  border-radius: 20px;
  border: 1px solid #ff6143;
  margin-top: 12%;
  padding: 10px;
  animation: modal 1s forwards;
}
@keyframes modal {
  from {
    opacity: 0;
    transform: translate3d(0, -200px, 0);
  }
  to {
    opacity: 1;
    transform: translate3d(0, 0px, 0);
  }
}
.modal_dados {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: "Roboto", sans-serif;
  font-style: normal;
  margin-top: 30px;
}
.title-modal {
  color: #eb3636;
  font-size: 36px;
  line-height: 42px;
  letter-spacing: 0.1em;
}
.description {
  margin: 20px 0 10px;
  font-size: 24px;
}
.modal img {
  max-width: 100%;
  margin: 0 auto;
  display: block;
}
.buttons {
  display: flex;
}
.button-modal {
  padding: 0.4rem 2.25rem;
  background-color: #ff6143;
  border-radius: 20px;
  border: 1px solid #ff6143;
  color: #fff;
  font-size: 18px;
  transition: all 0.3s;
  cursor: pointer;
  font-family: "Roboto", sans-serif;
  font-weight: 300;
  margin: 30px;
}
.button-modal:hover {
  background-color: white;
  color: #ff6143;
}
.modal::before {
  content: "";
  position: fixed;
  top: 0px;
  left: 0px;
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  z-index: 1;
}
@media (max-width: 768px) {
  .modal_container {
    width: 90%;
  }
}
</style>
