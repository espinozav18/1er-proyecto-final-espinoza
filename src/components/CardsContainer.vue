<template>
  <div class="alinear">
    <h2>Listado de productos</h2>
    <v-row>
      <v-col v-for="(prod, i) in productos" :key="i">
       <CardProductos
       :producto="prod"
       />
      </v-col>
    </v-row>
  </div>
</template>

<script>
import CardProductos from "./CardProductos.vue"
export default {
    components:{
CardProductos
    },
  props: {
    productos: Array,
  },
};
</script>

<style lang="scss" scoped>
.alinear{
 text-align: left;
}
</style>