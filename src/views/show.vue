<template>
  <div>
    <Modal v-if="carrinho" :carrinho.sync="carrinho"></Modal>
    <div class="banner-color" v-if="api" :id="api.id">
      <div class="produto-banner">
        <div class="container">
          <img class="imagem" v-bind:src="api.image">
          <div class="produto-content">
            <p class="title">{{api.title}}</p>
            <p class="description">{{api.description}}</p>
            <p class="price" v-if="api.promotional_price">
              de
              <span>R${{api.price}}</span>
              por
              <b>R${{api.promotional_price}}</b>
            </p>
            <p class="price" v-else>R${{api.price}}</p>
            <div class="sizes">
              <div v-for="(size, i) in api.sizes" :key="size + i">
                <input type="radio" :id="size" class="product__form_radio" name="size">
                <label :for="size" class="product__form__label">{{size}}</label>
              </div>
            </div>
            <button class="button-home" v-on:click="carrinho = true">Adicionar ao carrinho</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Modal from "@/components/Modal.vue";
export default {
  name: "produto",
  props: ["produto"],
  components: {
    Modal
  },
  data() {
    return {
      api: null,
      carrinho: false
    };
  },
  methods: {
    fetchData() {
      fetch(`http://localhost:3000/products/${this.produto}`)
        .then(response => response.json())
        .then(response => {
          this.api = response;
        });
      window.scrollTo({
        behavior: "smooth",
        top: 0
      });
    },
    
  },
  created() {
    this.fetchData();
  },
  watch: {
    $route: "fetchData"
  }
};
</script>

<style>
.sizes {
  display: flex;
  margin-top: 10px;
}
.product__form__label {
  width: 60px;
  height: 60px;
  margin-right: 1em;
  display: inline-block;
  border-radius: 50%;
  border: 1px solid #ff6143;
  text-align: center;
  line-height: 60px;
  transition: all 0.3s;
  cursor: pointer;
}
.product__form_radio {
  display: none;
}
.product__form_radio:checked + .product__form__label {
  color: #fff;
  background-color: #ff6143;
}

.imagem {
  height: 562px;
}
.banner-color {
  height: 100%;
  background-color: #efedef;
  width: 100%;
  position: relative;
}
.banner-color::before {
  content: "";
  background-image: url(../assets/images/confetti-banner.svg);
  background-repeat: no-repeat;
  position: absolute;
  background-size: 100%;
  top: -15%;
  width: 100%;
  height: 240px;
  max-height: 240px;
}
.produto-banner {
  display: flex;
  align-items: center;
  justify-content: center;
}
.container {
  width: 952px;
  max-width: 100%;
  display: flex;
  align-items: center;
}
.produto-banner .imagem {
  height: 100%;
  max-height: 562px;
}
.produto-content .title {
  font-size: 24px;
  font-weight: 300;
  line-height: 28px;
  margin-bottom: 20px;
}
.produto-content .description {
  font-size: 13px;
  line-height: 18px;
  letter-spacing: 0.1em;
  color: #565656;
}
.produto-content .price {
  margin-top: 20px;
  font-size: 24px;
  line-height: 28px;
  letter-spacing: 0.1em;
}
.produto-content .price span {
  text-decoration: line-through;
  font-weight: 300;
}
.produto-content .price b {
  font-weight: bold;
}

@media (max-width: 768px) {
  .container {
    padding: 0 8px;
  }
  .produto-banner .imagem {
    max-height: 250px;
  }
  .produto-content .title {
    font-size: 14px;
    line-height: 16px;
  }
  .produto-content .description {
    font-size: 10px;
    line-height: 13px;
  }
  .produto-content .price {
    font-size: 12px;
    line-height: 14px;
  }
  .banner-color::before {
    display: none;
  }
  .product__form__label {
    font-size: 12px;
    height: 30px;
    width: 30px;
    line-height: 30px;
  }
}
</style>
