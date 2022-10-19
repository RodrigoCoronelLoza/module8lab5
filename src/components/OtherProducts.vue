<template>
  <div class="container">
    <div class="row">
      <h4>Productos relacionados</h4>
    </div>
    <div class="row">
      <div
        class="col"
        @click="ChooseProduct(p.id)"
        v-for="p in productosCards"
        :key="p.id"
      >
        <div class="card" style="width: 18rem">
          <div class="card-body">
            <h5 class="card-title">{{ p.nombre }}</h5>
            <img :src="p.imagen" alt="" :style="`width: 100%`" />
            <p class="card-text" v-html="p.descripcion"></p>
            <div class="producto-relacionado-precio">
              Precio:{{ p.precio }} BOB
            </div>
            <div>
              <div style="display: flex">
                <div v-for="color of p.colores">
                  <div
                    class="color-box clic"
                    :style="`background:${color}`"
                  ></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "OtherProducts",

  data() {
    let productosCards;
    let productoant;
    return {
      productosCards,
      productoant,
      antId: "null",
    };
  },
  methods: {
    getOtherProducts() {
      axios({
        method: "get",
        url: "http://localhost:4040/Productos?preferido=false",
      })
        .then((response) => {
          this.productosCards = response.data;
          console.log(response);
        })
        .catch((e) => console.log(e));
    },

    getProducts() {
      axios({
        method: "get",
        url: "http://localhost:4040/Productos?preferido=true",
      })
        .then((response) => {
          this.productoant = response.data;
          console.log(this.productoant);
          this.antId = this.productoant[0].id;
          console.log(this.productoant[0].id);
        })
        .catch((e) => console.log(e));
    },
    ChooseProduct(clickId) {
      console.log(this.antId);
      this.ChangePreferidoToFalse(this.antId);
      this.ChangePreferidoToTrue(clickId);
      location.reload();
    },
    ChangePreferidoToFalse(id) {
      console.log(id);
      axios({
        method: "patch",
        url: "http://localhost:4040/Productos/" + id,
        data: { preferido: false },
      })
        .then((response) => {
          console.log(response);
        })
        .catch((e) => console.log(e));
    },

    ChangePreferidoToTrue(id) {
      console.log(id);
      axios({
        method: "patch",
        url: "http://localhost:4040/Productos/" + id,
        data: { preferido: true },
      })
        .then((response) => {
          console.log(response);
        })
        .catch((e) => console.log(e));
    },
  },
  mounted() {
    this.getOtherProducts();
    this.getProducts();
  },
  components: {},
};
</script>
