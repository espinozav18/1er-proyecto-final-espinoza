<template>
  <v-card class="pa-5">
    <v-card-title>
      Finaliza tu Compra - Disfrutas de tus productos
    </v-card-title>
    <v-card-text class="pa-5">
      <v-form ref="form" v-model="valid" lazy-validation>
        <v-row>
          <v-col cols="12" lg="6">
            <v-card>
              <v-card-title> Datos del Cliente </v-card-title>
              <v-card-text>
                <h4>Datos Personales</h4>
                <v-row>
                  <v-col cols="12" sm="6">
                    <v-text-field
                      v-model="cliente.nombre"
                      :rules="[(v) => !!v || 'Ingrese Nombres']"
                      label="Nombre"
                      required
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6">
                    <v-text-field
                      v-model="cliente.apellidos"
                      :rules="[(v) => !!v || 'Ingrese Apellidos']"
                      label="Apellidos"
                      required
                    ></v-text-field>
                  </v-col>
                </v-row>
                <v-row>
                  <v-col cols="12" sm="6">
                    <v-text-field
                      v-model="cliente.dni"
                      :type="'number'"
                      :rules="[
                        (d) => !!d || 'Ingrese dni',
                        (d) => /\d{8}/.test(d) || 'Dni debe tener 8 digitos',
                      ]"
                      label="Dni"
                      required
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6">
                    <v-text-field
                      v-model="cliente.telefono"
                      :type="'number'"
                      :rules="[
                        (d) => !!d || 'Ingrese telefono',
                        (d) =>
                          /\d{9}/.test(d) || 'telefono debe tener 9 digitos',
                      ]"
                      label="telefono"
                      required
                    ></v-text-field>
                  </v-col>
                </v-row>

                <v-text-field
                  v-model="cliente.direccion"
                  :rules="[(v) => !!v || 'Ingrese dirección']"
                  label="Dirección"
                  required
                ></v-text-field>
                <v-text-field
                  v-model="cliente.email"
                  disabled
                  :rules="[
                    (v) => !!v || 'Ingrese e-mail',
                    (v) =>
                      /.+@.+\..+/.test(v) || 'direccion de correo invalida',
                  ]"
                  label="Email"
                  required
                ></v-text-field>
                <h4>Datos de Tarjeta de pago</h4>

                <v-row>
                  <v-col cols="12" sm="6">
                    <v-text-field
                      v-model="cliente.titulartarjeta"
                      :rules="[(v) => !!v || 'Ingrese Titular Tarjeta']"
                      label="Titular Tarjeta"
                      required
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6">
                    <v-text-field
                      v-model="cliente.nrotarjeta"
                      :rules="[(v) => !!v || 'Ingrese Datos de tarjeta']"
                      label="Datos de tarjeta"
                      required
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      :return-value.sync="cliente.fechavencimiento"
                      transition="scale-transition"
                      offset-y
                      max-width="290px"
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          label="Fecha de vencimiento"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                          v-model="cliente.fechavencimiento"
                          :rules="[(v) => !!v || 'Fecha de vencimiento']"
                          required
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="cliente.fechavencimiento"
                        type="month"
                        no-title
                        scrollable
                      >
                        <v-spacer></v-spacer>
                        <v-btn text color="primary" @click="menu = false">
                          Cancel
                        </v-btn>
                        <v-btn
                          text
                          color="primary"
                          @click="$refs.menu.save(cliente.fechavencimiento)"
                        >
                          OK
                        </v-btn>
                      </v-date-picker>
                    </v-menu>
                    <!-- <v-text-field
                    v-model="cliente.fechavencimiento"
                    :type="'date'"
                    :rules="[(v) => !!v || 'Fecha de vencimiento']"
                    label="Fecha de vencimiento"
                    required
                  ></v-text-field>-->
                  </v-col>
                  <v-col cols="12" sm="6">
                    <v-text-field
                      v-model="cliente.codigocvv"
                      :rules="[(v) => !!v || 'Ingrese CVV']"
                      label="CVV"
                      required
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-card-text>
            </v-card>
          </v-col>
          <v-col cols="12" lg="6">
            <v-card>
              <v-card-title> Lista de productos </v-card-title>
              <v-card-text>
                <ListaCarrito :listaProductos="carrito" />
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-form>
    </v-card-text>
    <v-card-actions class="justify-end">
      <v-btn color="error" text @click="dialog = false">Cerrar</v-btn>
      <v-btn color="success" :disabled="!valid" class="mr-1" @click="comprar">
        Pagar S/ <span class="total-pagar"> {{ totalPagar }}</span>
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
import ListaCarrito from "../components/ListaCarrito.vue";
export default {
  components: {
    ListaCarrito,
  },
  props: {
    listaProductos: Array,
    cantItem: Number,
  },
  data() {
    return {
      carrito: [
        {
          nro: 1,
          id: 15,
          nombre: "Teclado",
          marca: "Logitech",
          precio: 150,
          cantidad: 3,
          total: 150 * 3,
        },
        {
          nro: 2,
          id: 16,
          nombre: "Impresora",
          marca: "Epson",
          precio: 200,
          cantidad: 4,
          total: 200 * 4,
        },
      ],

      cliente: {
        id: 0,
        nombre: "",
        apellidos: "",
        dni: "",
        telefono: "",
        direccion: "",
        email: "",
        titulartarjeta: "",
        nrotarjeta: "",
        fechavencimiento: "",
        codigocvv: "",
      },

      menu: false,
      modal: false,
      valid: true,
      mensaje: "",
      mensajeRegistro: "",
    };
  },
  computed: {
    totalPagar() {
      return this.carrito.reduce((a, b) => a + b.total, 0);
    },
  },
  methods: {
    comprar() {
      const validar = this.$refs.form.validate();
      if (validar) {
        console.info("Compra exitosa");
      } else {
        console.info("Error Compra");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.a-router {
  color: white;
  font-weight: bold;
  text-decoration: none;
}
.total-pagar {
  color: #d50000;
  font-weight: bold;
}
.align-text {
  text-align: end !important;
}
</style>
