<template>
<v-row class="pa-6">
    <v-col cols="12" sm="5">
        <v-card class="pa-2" tile>
            <v-card-title>Registro Productos
                
            </v-card-title>
            <v-card-text>
                <CrearProducto />
            </v-card-text>
        </v-card>
    </v-col>
    <v-col cols="12" sm="7">
        <v-card class="pa-2" tile>
            <v-card-title>Productos </v-card-title>

            <v-card-text>
                <TablaProductos />
            </v-card-text>
        </v-card>
    </v-col>
</v-row>
</template>

<script>
import TablaProductos from "../../components/TablaProductos.vue";
import CrearProducto from "../../components/CrearProducto.vue";

export default {
    components: {
        TablaProductos,
        CrearProducto,
    },
    data() {
        return {
          
        };
    },
    mounted() {

    },
    methods: {

    },
};
</script>

<style lang="scss" scoped>
</style>
