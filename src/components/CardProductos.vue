
<template>
  <v-card hover max-height="520" min-height="520" class="alinear">
    <v-card-title>
      <v-img
        height="250"
        width="200px"
        :src="producto.imagenes[0]"
      />
      {{ producto.nombre }}
    </v-card-title>

    <v-card-text>
      <p>Precio: <strong>{{ producto.moneda }} {{ producto.precio |decimal2}}</strong></p>
      <p>Cantidad: {{ producto.stock }}</p>
      
    </v-card-text>
    <v-card-actions>
      <BotonComprar    :producto="producto" />
      <v-spacer></v-spacer>
      <DetalleProduco :producto="producto" />
    </v-card-actions>
  </v-card>
</template>

<script>
import DetalleProduco from "./DetalleProducto.vue"
import BotonComprar from "./BotonComprar.vue"
export default {
  components:{
    DetalleProduco,
    BotonComprar
  },
  props: {
    producto: Object,
  },
  filters:{
    decimal2(value){
      return value.toFixed(2)
    }
  }
};
</script>

<style lang="scss" scoped>
.alinear{
 text-align: left;
}
</style>