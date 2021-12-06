<template>
  <v-dialog v-model="dialog" persistent max-width="500">
    <template v-slot:activator="{ on, attrs }">
      <v-btn icon v-bind="attrs" v-on="on" @click="mensaje = '',registroUsuario=false" v-show="login">
        <v-icon>mdi-account</v-icon>
      </v-btn>
      <v-list color="bar-fondo" v-show="login">
        <v-list-item class="bgsel" link>
          <v-list-item-title v-bind="attrs" v-on="on" @click="mensaje = '',registroUsuario=true">Registrar</v-list-item-title>
        </v-list-item>
      </v-list>
      <v-menu offset-y>
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            v-show="login == false"
            dark
            class="text-capitalize mr-2"
            color="blue"
            v-bind="attrs"
            v-on="on"
          >
            <v-list-item-title to="/" class="flm"
              ><v-icon>mdi-account-cog</v-icon> Juan</v-list-item-title
            >
          </v-btn>
        </template>
        <v-list>
          <v-list-item
            v-for="(item, index) in items"
            :key="index"
            class="bgsel"
            link
          >
            <v-list-item-title @click="login = true">{{
              item.title
            }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </template>
    <v-card v-if="!registroUsuario">
      <v-card-title class="text-h5"> Iniciar Sessión </v-card-title>
      <v-card-text>
        <v-form ref="form" v-model="valid" lazy-validation>
          <v-text-field
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
          ></v-text-field>
          <v-text-field
            v-model="password"
            maxlength="16"
            :rules="passwordRules"
            :type="'password'"
            label="Password"
            required
          ></v-text-field>
          <v-alert v-if="mensaje !== ''" dense outlined type="error">
            {{ mensaje }}
          </v-alert>
        </v-form>
      </v-card-text>
      <v-card-actions offset-y>
        <v-spacer></v-spacer>
        <v-btn color="error" class="mr-4" @click="dialog = false">
          Cancelar
        </v-btn>
        <v-btn
          :disabled="!valid"
          color="success"
          class="mr-4"
          @click="validate"
        >
          Ingresar
        </v-btn>
      </v-card-actions>
    </v-card>
    <registroUsuario @cerrarDialog="cerrarDialogs($event)" v-else/>
  </v-dialog>
</template>

<script>
import usuarios from "../assets/json/usuario.json";
import registroUsuario from "./RegistroUsuario.vue";
export default {
  components: {
    registroUsuario,
    
  },
  /* props:{
    mensajes:{type:Boolean}
  },*/
  data: () => ({
    usuario: usuarios,
    items: [{ title: "Cerrar" }],
    login: true,
    mensaje: "",
    dialog: false,//mostra dialog
    valid: true,
    registroUsuario:false,//mostrar formulario login
    password: "Coders2021",
    passwordRules: [
      (v) => !!v || "Contraseña",
      (v) =>
        /^(?=\w*\d)(?=\w*[A-Z])(?=\w*[a-z])\S{8,16}/.test(v) ||
        "La contraseña debe tener al entre 8 y 16 caracteres, al menos un dígito, al menos una minúscula y al menos una mayúscula.",
      //(v) => /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[$@$!%*?&])[A-Za-z\d$@$!%*?&]{8,15}[^'\s]/.test(v) || "Name must be less than 10 characters",
    ],
    email: "coderhouse@gmail.com",
    emailRules: [
      (v) => !!v || "E-mail",
      (v) => /.+@.+\..+/.test(v) || "E-mail no es valido",
    ],
  }),

  methods: {
    /*estadoLogin(){
          this.$emit("estLogin",true);
          //console.log("Entra al metodo");
      },
    */
    cerrarDialogs(param) {
      this.registroUsuario=param.registroUsuario;
      this.dialog=param.dialog;
      
    },
    validate() {
      const validar = this.$refs.form.validate();

      if (validar) {
        const validUsuario = this.usuario.find(
          (user) =>
            user.usuario === this.email && user.password === this.password
        );
        if (validUsuario !== undefined) {
          this.dialog = false;
          this.login = false;
          //console.info(this.login);
          //estadoLogin = this.estadoLoginM($event);
        } else {
          this.mensaje = "Usuario no encontrado";
        }
      }
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },
  },
};
</script>

<style lang="scss" scoped>
.bar-fondo {
  background-color: #3d5afe !important;
}
</style>
