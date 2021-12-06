<template>
  <v-dialog v-model="dialog" persistent max-width="500">
    <template v-slot:activator="{ on, attrs }">
      <v-btn icon v-bind="attrs" v-on="on">
        <v-badge color="green" v-if="cantItem > 0" :content="cantItem">
          <v-icon>mdi-cart</v-icon>
        </v-badge>
        <v-icon v-else>mdi-cart</v-icon>
      </v-btn>
    </template>
    <v-card>
      <v-toolbar color="primary" dark>Lista de productos</v-toolbar>
      <v-card-text>
        <v-data-table 
          :headers="carritoHeaders"
          :items="carrito"
          hide-default-footer
          class="elevation-1,pa-4"
        ><template v-slot:item.cantidad="{ item }">
            <v-text-field
            v-model="item.cantidad"
            v-on:input="item.total=item.cantidad*item.precio"
            label="cantidad"
            required
          ></v-text-field>
  
    </template></v-data-table>
      </v-card-text>
      <v-card-actions class="justify-end">
        <v-btn color="error" text @click="dialog = false">Cerrar</v-btn>
        <v-btn
         
          color="success"
          class="mr-4"
         
        >
          Pagar
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: {
    listaProductos: Array,
    cantItem: Number,
  },
  data() {
    return {
         dialog: false,//mostra dialog
      carritoHeaders: [
        { text: "Nombre ", value: "nombre" },
        { text: "Marca ", value: "marca" },
        { text: "Precio", value: "precio" },
        { text: "Cantidad", value: "cantidad" },
        { text: "Total", value: "total" },
      ],
      carrito: [
        {
          nombre: "Teclado",
          marca:"Logitech",
          precio: 150,
          cantidad: 3,
          total:150*3
        },
        {
          nombre: "Impresora",
          marca:"Epson",
          precio: 200,
          cantidad: 4,
          total:200*4
        },
      ],
    };
  },
  methods:{
      
  }
};
</script>

<style lang="scss" scoped>
</style>
