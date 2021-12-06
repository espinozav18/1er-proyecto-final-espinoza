<template>
  <v-app>
    <Menu :titulo="nombreTienda"  :cantItem="cantItems" />
    <Carrusel />
    <v-main>
      <v-container>
        <v-row class="mt-12">
          <v-col>
            <CardsContainer :productos="listProductos"  />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
    <Footer :titulo="nombreTienda" />
  </v-app>
</template>

<script>
import listaProd from "./assets/json/productos.json";
import Menu from "./components/Menu.vue";
import Footer from "./components/Footer.vue";
import Carrusel from "./components/Carrusel.vue";
import CardsContainer from "./components/CardsContainer.vue";

export default {
  name: "App",

  components: {
    Menu,
    Footer,
    Carrusel,
    CardsContainer,
  },

  data: () => ({
    nombreTienda: "Tienda Store",
    listProductos: listaProd,
    cantItems:0,
  }),
  
  methods: {

  },
};
</script>

<style lang="scss" scoped>
</style>
