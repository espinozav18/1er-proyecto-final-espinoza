<template>
  <v-card dark>
    <v-toolbar color="bar-fondo">
      <v-app-bar-nav-icon
        @click="drawer = true"
        v-if="$vuetify.breakpoint.xsOnly"
      >
      </v-app-bar-nav-icon>
      <v-app-bar-nav-icon v-else
        ><v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="../assets/tienda.png"
          transition="scale-transition"
          width="40"
      /></v-app-bar-nav-icon>

      <v-toolbar-title
        :class="{
          '': $vuetify.breakpoint.smAndDown,
          'ml-6': $vuetify.breakpoint.mdAndUp,
        }"
      >
        {{ titulo }}
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn
        dark
        class="text-capitalize mr-2"
        v-show="$vuetify.breakpoint.lgOnly"
        color="bar-fondo"
      >
        <v-list-item-title to="/" class="flm">Home</v-list-item-title>
      </v-btn>

      <v-btn
        dark
        v-show="$vuetify.breakpoint.lgOnly"
        class="text-capitalize"
        color="bar-fondo"
      >
        <v-list-item-title to="/productos" class="flm"
          >Productos</v-list-item-title
        >
      </v-btn>

      <v-btn
        color="bar-fondo"
        dark
        class="text-capitalize mr-14"
        v-show="$vuetify.breakpoint.lgOnly"
      >
        <v-list-item-title to="/contacto" class="flm"
          >Contacto</v-list-item-title
        >
      </v-btn>
      <Login />
      <Carrito :cantItem="cantItem" />
    </v-toolbar>

    <v-navigation-drawer
      v-model="drawer"
      absolute
      width="100%"
      height="auto"
      temporary
    >
      <v-list nav dense color="bar-fondo">
        <v-list-item-group v-model="group">
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>
            <v-list-item-title>
              <v-list-item-title to="/" class="flm">Home</v-list-item-title>
            </v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-store</v-icon>
            </v-list-item-icon>
            <v-list-item-title>
              <v-list-item-title to="/productos" class="flm"
                >productos</v-list-item-title
              >
            </v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-earth</v-icon>
            </v-list-item-icon>
            <v-list-item-title>
              <v-list-item-title to="/contacto" class="flm"
                >Contacto</v-list-item-title
              >
            </v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
  </v-card>
</template>


<script>
import Login from "./Login.vue";
import Carrito from "./Carrito.vue";
export default {
  name: "Menu",

  components: {
    Login,
    Carrito,
  },
  props: {
    titulo: String,
    cantItem: Number,
  },

  data() {
    return {
      drawer: false,
      group: null,
    };
  },

  methods: {},
};
</script>


<style lang="scss" scoped>
.bgsel:hover {
  background: #afaeae;
}

.flm:link {
  text-decoration: none;
}

.v-application a {
  color: #ffffff !important;
}
.bar-fondo {
  background-color: #3d5afe !important;
}
</style>