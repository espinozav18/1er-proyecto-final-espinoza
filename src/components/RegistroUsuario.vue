<template>
  <v-card>
    <v-card-title class="text-h5"> Registrar Usuario </v-card-title>
    <v-card-text>
      <v-form ref="form" v-model="valid" lazy-validation>
        <v-row>
          <v-col cols="12" sm="6">
            <v-text-field
              v-model="nombre"
              :rules="[() => !!nombre || 'Ingrese Nombres']"
              label="Nombre"
              required
            ></v-text-field>
          </v-col>
          <v-col cols="12" sm="6">
            <v-text-field
              v-model="apellidos"
              :rules="[() => !!apellidos || 'Ingrese Apellidos']"
              label="Apellidos"
              required
            ></v-text-field>
          </v-col>
          <v-col cols="12" sm="6">
            <v-text-field
              v-model="fechanacimiento"
              :type="'date'"
              :rules="[() => !!fechanacimiento || 'Fecha de nacimiento']"
              label="Fecha de nacimiento"
              required
            ></v-text-field>
          </v-col>
          <v-col cols="12" sm="6">
            <v-text-field
              v-model="dni"
              :type="'number'"
              :rules="[() => !!dni || 'Ingrese dni',
              () => (dni.length!=8) || 'Dni debe tener 8 digitos']"
              label="Dni"
              required
            ></v-text-field>
          </v-col>
        </v-row>

        <v-text-field
          v-model="direccion"
          :rules="[
            () => !!direccion || 'Ingrese dirección',
          ]"
          label="Dirección"
          required
        ></v-text-field>
        <v-text-field
          v-model="email"
          :rules="[
            (v) => !!v || 'Ingrese e-mail',
            (v) =>
              /.+@.+\..+/.test(v) ||
              'direccion de correo invalida',
          ]"
          label="Email"
          required
        ></v-text-field>
        <v-row>
          <v-col cols="12" sm="6">
            <v-text-field
              v-model="password"
              maxlength="16"
              :type="'password'"
              :rules="[
                (v) => !!v || 'Ingrese contraseña',
                (v) =>
                  /^(?=\w*\d)(?=\w*[A-Z])(?=\w*[a-z])\S{8,16}/.test(v) ||
                  'La contraseña debe tener al entre 8 y 16 caracteres, al menos un dígito, al menos una minúscula y al menos una mayúscula.',
              ]"
              label="contraseña"
              required
            ></v-text-field>
          </v-col>
          <v-col cols="12" sm="6">
            <v-text-field
              v-model="password2"
              maxlength="16"
              :type="'password'"
              :rules="[
                (v) => !!v || 'Ingrese contraseña',
                (v) => v === password || 'Contrase es diferente',
              ]"
              label="repetir contraseña"
              required
            ></v-text-field>
          </v-col>
        </v-row>
      </v-form>
    </v-card-text>
    <v-divider class="mt-12"></v-divider>
    <v-card-actions>
      <v-btn color="error" @click="ocultarDialog(0)"> Cancelar </v-btn>
      <v-spacer></v-spacer>
      <v-btn color="primary" @click="ocultarDialog(1)"> Registrar </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      nombre: "",
      apellidos: "",
      fechanacimiento: "",
      dni: "",
      direccion: "",
      email: "",
      password: "",
      password2: "",
      valid: true,
    };
  },
  methods: {
    ocultarDialog(param) {
      if (param == 0) {
          this.$emit("cerrarDialog", {"registroUsuario":false,"dialog":false});
      } else {
        const validar = this.$refs.form.validate();
        if (validar) {
          this.$emit("cerrarDialog", {"registroUsuario":false,"dialog":true});
        }
      }
    },
    validate() {
      this.$refs.form.validate();

      /* if (validar) {
          
      }*/
    },
    reset() {
      this.$refs.form.reset();
    },
  },
};
</script>

<style lang="scss" scoped>
</style>