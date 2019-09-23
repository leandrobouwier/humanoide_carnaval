<template>
  <div class="produtos">
    <p class="introducao">
      Se você comprar eu te dou um
      <span>
        <b>beijo</b> (só se quixer)
      </span>
    </p>
    <div class="grid">
      <ul class="produto">
        <li v-for="(produto) in api" :key="produto.id" :id="produto.id">
          <img class="img" v-bind:src="produto.image">
          <div class="preco">
            <h1 class="promotional" v-if="produto.promotional_price">
              de
              <span>R${{produto.price}}</span>
              por R${{produto.promotional_price}}
            </h1>
            <h1 v-else>R${{produto.price}}</h1>

            <router-link
              class="button-home"
              tag="button"
              :to="{name:'show', params: {produto: produto.id}}"
            >Mais detalhes</router-link>
          </div>
        </li>
      </ul>
    </div>
    <div class="texte"></div>
  </div>
</template>

<script>
export default {
  name: "Produtos",
  data() {
    return {
      api: null
    };
  },
  methods: {
    fetchData() {
      fetch("http://localhost:3000/products")
        .then(response => response.json())
        .then(response => {
          this.api = response;
        });
    }
  },
  created() {
    this.fetchData();
  }
};
</script>

<style>
.produtos {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin-top: 50px;
}
.introducao span {
  color: #ff6143;
}
.introducao b {
  font-weight: bold;
}
.grid {
  display: flex;
  max-width: 1024px;
}
.produto {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  cursor: pointer;
  height: 500px;
  margin-top: 18px;
}
.produto li {
  padding: 20px 10px;
}
.produto li:hover {
  box-sizing: border-box;
  box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.25);
  padding: 20px 10px;
  transition-duration: 1s;
  transition-timing-function: ease-in-out;
  display: block;
}

.produto li:hover .preco {
  display: block;
  transition-duration: 1s;
  transition-timing-function: ease-in-out;
}

.produto img {
  cursor: initial;
}
.produto .preco {
  margin-top: 0.5em;
  text-transform: uppercase;
  display: none;
}

.produto .promotional span {
  text-decoration: line-through;
}
.produto .button-home {
  margin-top: 0.5em;
}

@media (max-width: 768px) {
  .produto .preco h1 {
    font-size: 12px;
  }
  .produto {
    height: 100%;
  }
  .produto li:hover {
    box-shadow: initial;
    padding: 20px 10px;
  }
  .produto .preco {
    display: block;
  }
}
</style>
