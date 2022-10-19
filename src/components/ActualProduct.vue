<template>
  <div class="container" v-for="p in productoShow" :key="p.id">
    <div class="row">
      <h3>{{ p.nombre }}</h3>
    </div>
    <div class="row">
      <div class="col-12 col-sm-6 col-md-4">
        <img :style="`width: 100%`" :src="p.imagen" alt=" " />
      </div>
      <div class="col-12 col-sm-6 col-md-8">
        <h6 v-html="p.descripcion"></h6>
        <div
          class="p-3 mb-2 text-white"
          :style="`background: orangered;color:white;font-weight:bold`"
        >
          Precio: {{ p.precio }} BOB
        </div>
        <h5>Color</h5>
        <div style="display: flex">
          <div v-for="color of p.colores">
            <div
              class="color-box clic"
              @click="ColorClick(`${color}`, `${p.id}`)"
              :style="`background:${color}`"
            ></div>
          </div>
        </div>

        <h5>Cantidad</h5>
        <div class="quantity">
          <button v-on:click="decrementCounter()">-</button>
          <div>{{ compteur }}</div>
          <button v-on:click="incrementCounter()">+</button>
        </div>

        <div class="buy-box">
          <button
            type="button"
            class="btn btn-primary"
            v-on:click.once="EventoComprar()"
          >
            Comprar
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ActualProduct",

  data() {
    let productoShow;

    return {
      productoShow,
      cantidad: 1,
      colorSelect: null,
      compteur: 0,
      actualId: null,
    };
  },
  methods: {
    getProducts() {
      axios({
        method: "get",
        url: "http://localhost:4040/Productos?preferido=true",
      })
        .then((response) => {
          this.productoShow = response.data;
          console.log(response);
        })
        .catch((e) => console.log(e));
    },
    ColorClick: function (mensaje, id) {
      alert("eligio:".concat(mensaje));
      this.colorSelect = mensaje;
      this.actualId = id;
      console.log(this.actualId);
    },
    incrementCounter() {
      return this.compteur++;
    },
    decrementCounter() {
      if (this.compteur >= 1) {
        return this.compteur--;
      } else {
        return this.compteur;
      }
    },
    EventoComprar() {
      if (this.compteur >= 1 && this.colorSelect) {
        alert(
          `{id: ${this.actualId}, cantidad : ${this.compteur},color: ${this.colorSelect}}`
        );
      }
    },
  },
  mounted() {
    this.getProducts();
  },
  components: {},
};
</script>
