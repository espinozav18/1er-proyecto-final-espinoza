<template>
  <div>
    <v-data-table
      :headers="carritoHeaders"
      :items="carritoItem"
      hide-default-footer
      class="elevation-1,pa-4"
    >
      <template v-slot:item.cantidad="{ item }">
        <v-text-field
          :type="'number'"
          v-model="item.cantidad"
          v-on:input="item.total = item.cantidad * item.precio"
           :rules="[(v) => !!v || 'Ingrese cantidad']"
          label="cantidad"
          class="align-text"
          required
        ></v-text-field>
      </template>
      <template v-slot:item.acciones="{ item }">
        <v-icon color="error" medium @click="deleteItem(item)">
          mdi-delete
        </v-icon>
      </template></v-data-table
    >
    <v-dialog v-model="dialogDelete" max-width="500px">
      <v-card>
        <v-card-title class="text-h5"
          >Esta seguro de Eliminar este Item?</v-card-title
        >
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="error darken-1" @click="closeDelete">no</v-btn>
          <v-btn color="success darken-1" @click="deleteItemConfirm">si</v-btn>
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: {
    listaProductos: Array,
    
  },
  mounted(){
      this.carritoItem=this.$props.listaProductos
  },
  data() {
    return {
      dialogDelete: false,
      idDelete: 0,
      carritoHeaders: [
        { text: "#", value: "nro" },
        { text: "Nombre ", value: "nombre" },
        { text: "Marca ", value: "marca" },
        { text: "Precio", value: "precio", align: "right" },
        { text: "Cantidad", value: "cantidad" },
        { text: "Total", value: "total", align: "right" },
        { text: "Acciones", value: "acciones" },
      ],
      carritoItem:[]
    };
  },
  methods: {
    deleteItem(item) {
      this.idDelete = this.carritoItem.indexOf(item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.carritoItem.splice(this.idDelete, 1);
      this.closeDelete();
    },
    closeDelete() {
      this.dialogDelete = false;
    },
  },
};
</script>

<style lang="scss" scoped>
</style>