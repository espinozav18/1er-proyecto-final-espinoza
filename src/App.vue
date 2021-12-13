<template>
 <v-app>
 <Menu :titulo="nombreTienda" :cantItem="cantItems" />
    
    <!--<div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>-->
    <router-view />
    <Footer :titulo="nombreTienda" />
 </v-app>

   
 
</template>

<script>
//import listaProd from "./assets/json/productos.json";
import Menu from "./components/Menu.vue";
import Footer from "./components/Footer.vue";
//const axios = require("axios");
export default {
  name: "Home",
  components: {
    Menu,
    Footer,
  },
  data: () => ({
    nombreTienda: "Tienda Store",
    //listProductos: [],
    cantItems: 0,
  }),
  mounted(){
    //this.listaProductos();
  },
  methods:{
   /* async listaProductos(){
      await axios
          .get(`https://61b75f4e64e4a10017d18ae0.mockapi.io/productos`, {})
          .then((rpta) => {
            if (rpta.status == 201 || rpta.status == 200) {
              this.listProductos=rpta.data;
            }
          }).catch(error => { this.mensaje = error.response.status + ": " + error.message;  });
    }*/
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
