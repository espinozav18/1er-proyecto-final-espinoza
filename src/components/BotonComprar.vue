<template>
  <v-btn
    color="success"
    v-if="producto.stock > 0"
    @click="comprarItem(producto)"
    ><v-icon>mdi-cart-plus </v-icon>Comprar</v-btn
  >
  <v-chip v-else dark>Sin stock</v-chip>
</template>

<script>
//import Menu from "./Menu.vue";
export default {
  name: "BotonComprar",
  //extends: Menu,
  props: {
    producto: Object,
  },
  data() {
    return {};
  },

  methods: {
    comprarItem(prod) {
      this.$listaCarrito.push({
        nombre: prod.nombre,
        marca: prod.marca,
        modelo: prod.modelo,
        precio: prod.precio,
        cantidad: 1,
        total: prod.precio * 1,
      });
      console.info(this.$listaCarrito);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>