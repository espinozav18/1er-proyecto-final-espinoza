<template>
  <div class="home">
    <Carrusel />
    <v-container>
      <v-row class="mt-12">
        <v-col>
          <CardsContainer :productos="listProductos" />
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
//import listaProd from "../assets/json/productos.json";
import Carrusel from "../components/Carrusel.vue";
import CardsContainer from "../components/CardsContainer.vue";
const axios = require("axios");
export default {
  name: "Home",
  components: {
    Carrusel,
    CardsContainer,
    //  HelloWorld
  },
   data: () => ({
   
    listProductos: [],

  }),
   mounted(){
    this.listaProductos();
  },
  methods:{
    async listaProductos(){
      await axios
          .get(`https://61b75f4e64e4a10017d18ae0.mockapi.io/productos`, {})
          .then((rpta) => {
            if (rpta.status == 201 || rpta.status == 200) {
              this.listProductos=rpta.data;
            }
          }).catch(error => { this.mensaje = error.response.status + ": " + error.message;  });
    }
  }
};
</script>
