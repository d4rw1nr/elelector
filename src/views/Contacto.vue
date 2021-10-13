<template>
    <v-card
        class="mx-auto"
        max-width="500"
    >
        <v-img
        class="white--text align-end"
        height="200px"
        src="https://kinsta.com/es/wp-content/uploads/sites/8/2018/02/marketing-por-correo-electr%C3%B3nico-1-1024x512.png"
        >
        <v-card-title id="titulos">Contactenos</v-card-title>
        </v-img>

        <!---FORMATOS DE INPUTS-->
    <v-form id="margen" ref="form" v-model="valid" lazy-validation>
    
    <v-text-field
      v-model="nombre"
      :rules="[v => !!v || 'Escriba su nombre completo']"
      label="Nombre completo"
    ></v-text-field>

    <v-text-field
      v-model="email"
      :rules="[v => !!v || 'Escriba un correo válido']"
      label="E-mail"
      required
    ></v-text-field>

    <v-textarea
          v-model="textSolicitud"
          outlined
          :rules="[v => !!v || 'Escriba una descripción de su solicitud']"
          name="input-7-4"
          label="Describa su solicitud"
        ></v-textarea>

    <v-checkbox
      v-model="checkbox"
      :rules="[v => !!v || 'Debe aceptar el uso de tratamiento de datos para continuar']"
      label="Acepta el uso de tratamiento de datos?"
      required
    ></v-checkbox>

    <br>
    <v-btn
      :disabled="!valid"
      color="success"
      class="mr-4"
      @click="validar"
    >
      Enviar
    </v-btn>

    <v-btn
      color="error"
      class="mr-4"
      @click="borrar"
    >
      Borrar datos
    </v-btn>

    
  </v-form>
  <br>
        <!--FIN DE FORMATO DE INPUTS-->
    </v-card>
</template>

<script>

export default {
  data: ()=>{
    return{
    nombre: '',
    email: '',
    solicitud: '',
    textSolicitud: '',
    }
  },

  methods: {
    borrar(){
      this.nombre = '';
      this.email = '';
      this.solicitud = '';
      this.textSolicitud = ''
    },
    
  }
}

</script>

<style>
#margen{
  margin: 15px;
}
</style>