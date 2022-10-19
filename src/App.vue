<template>
  <Menu></Menu>
  <ActualProduct></ActualProduct>
  <OtherProducts></OtherProducts>
  <Foot></Foot>
</template>

<script>
import Menu from "./components/Menu.vue";
import ActualProduct from "./components/ActualProduct.vue";
import OtherProducts from "./components/OtherProducts.vue";
import Foot from "./components/Foot.vue";

export default {
  name: "App",
  components: {
    Menu,
    ActualProduct,
    OtherProducts,
    Foot,
  },
  methods: {},
  computed: {},
  mounted() {},
};
</script>

<style></style>
