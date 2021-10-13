<template>
  <div @update="showCandidates()">
    <v-layout wrap>
      <v-flex xs2>
        <v-toolbar color="black"></v-toolbar>
      </v-flex>
      <v-flex xs8>
        <v-toolbar color="black" dark>
          <v-spacer></v-spacer>
          <v-toolbar-title>
            <v-btn text @click="showCadidates()">
              CLICK PARA ACTUALIZAR TABLA DE CANDIDATOS
            </v-btn>
          </v-toolbar-title>
          <v-spacer></v-spacer>
        </v-toolbar>
      </v-flex>
      <v-flex xs2>
        <v-toolbar color="black">
          <v-row justify="center">
            <v-dialog
              v-model="dialog"
              persistent
              max-width="600px"
              ref="dialogForm"
            >
              <template v-slot:activator="{ on }">
                <v-btn
                  color="white"
                  v-on="on"
                  @click="addModeButton(), clearForm()"
                >
                  Agregar candidato</v-btn
                >
              </template>
              <v-form ref="forCandidate" v-model="valid" lazy-validation>
                <v-card>
                  <v-card-title>
                    <span class="text-h5">PERFIL DEL CANDIDATO</span>
                  </v-card-title>
                  <v-card-text>
                    <v-container>
                      <v-row>
                        <v-col cols="12">
                          <v-text-field
                            label="Nombre*"
                            v-model="nombre"
                            ref="nombre"
                            :rules="[
                              (v) => !!v || 'Se requiere poner un nombre',
                            ]"
                            value="qwert"
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6" md="6">
                          <v-text-field
                            label="Edad*"
                            ref="edad"
                            v-model="edad"
                            :rules="[
                              (v) => !!v || 'Se requiere poner una edad',
                            ]"
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="12" md="6">
                          <v-autocomplete
                            label="Partido*"
                            ref="partido"
                            v-model="partido"
                            :rules="partidoRules"
                            required
                            :items="[
                              'Sin partido/Independiente',
                              'Partido Liberal Colombiano',
                              'Partido Conservador Colombiano',
                              'Movimiento Autoridades Indígenas de Colombia AICO',
                              'Nuevo Liberalismo',
                              'Unión Patriótica UP',
                              'Partido Alianza Social Independiente ASI',
                              'Partido Cambio Radical',
                              'Partido Político Mira',
                              'Partido Social de Unidad Nacional “Partido de la U”',
                              'Partido Alianza Verde',
                              'Partido Polo Democrático Alternativo',
                              'Movimiento Colombia Humana',
                              'Partido Centro Democrático',
                              'Movimiento Alternativo Indígena y Social MAIS',
                              'Comunes',
                              'Partido Colombia Justa Libres',
                              'Partido Colombia Renaciente',
                              'Partido ADA',
                              'Partido Dignidad',
                            ]"
                          >
                          </v-autocomplete>
                        </v-col>
                        <v-col cols="12" sm="6" md="6">
                          <v-text-field
                            label="Profesión*"
                            ref="profesion"
                            v-model="profesion"
                            :rules="[
                              (v) => !!v || 'Se requiere poner una profesión',
                            ]"
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6" md="12">
                          <v-text-field
                            label="Perfil*"
                            ref="perfil"
                            v-model="perfil"
                            :rules="[
                              (v) => !!v || 'Se requiere poner un perfil',
                            ]"
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6" md="12">
                          <v-text-field
                            label="Educación*"
                            ref="educacion"
                            v-model="educacion"
                            :rules="[
                              (v) =>
                                !!v ||
                                'Se requiere poner la educación del candidato',
                            ]"
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12" sm="6" md="12">
                          <v-text-field
                            label="Cargos*"
                            ref="cargos"
                            v-model="cargos"
                            :rules="[
                              (v) => !!v || 'Se requiere poner los cargos',
                            ]"
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                          <v-text-field
                            label="Sigep*"
                            ref="sigep"
                            v-model="sigep"
                            :rules="[
                              (v) => !!v || 'Se requiere poner el sigep',
                            ]"
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                          <v-text-field
                            label="Imagen*"
                            ref="imagen"
                            v-model="imagen"
                            :rules="[
                              (v) => !!v || 'Se requiere poner una imagen',
                            ]"
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                          <v-file-input
                            show-size
                            counter
                            ref="ir"
                            v-model="ir"
                            chips
                            multiple
                            label="Dé click e inserte la imagen"
                            class="accept='image/*'"
                            @change="validatePicture"
                          ></v-file-input>
                        </v-col>
                      </v-row>
                    </v-container>
                    <small>*indica campo obligatorio</small>
                  </v-card-text>
                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn
                      color="blue darken-1"
                      submit
                      text
                      @click="dialog = false"
                    >
                      Cerrar
                    </v-btn>
                    <v-btn
                      :disabled="!valid"
                      v-model="btnSave"
                      color="blue darken-1"
                      text
                      @click="(dialog = false), validate()"
                    >
                      Guardar
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-form>
            </v-dialog>
          </v-row>
        </v-toolbar>
      </v-flex>
      <v-flex xs12>
        <v-data-table
          style="font-family: 'Open Sans', sans-serif
          font-size: 1rem;
          "
          ref="alv"
          dark
          :headers="headers"
          :items="candidates"
          class="elevation-1"
        >
          <template v-slot:[`item.actionsE`]="{ item }">
            <v-btn
              color="blue"
              @click="edit(item._id), (dialog = true), (idKey = item._id)"
            >
              {{ item.actions }}
              <v-icon>mdi-pencil</v-icon>
            </v-btn>
          </template>
          <template v-slot:[`item.actionsRe`]="{ item }">
            <v-btn
              color="red"
              @click="
                (dialogDelete = true), activateDelete(), (idKey = item._id)
              "
            >
              {{ item.actions }}
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </template>
        </v-data-table>
      </v-flex>
    </v-layout>
    <v-row justify="space-around">
      <v-col cols="auto">
        <v-dialog v-model="dialogDelete" width="500">
          <v-card>
            <v-card-title class="text-h5 grey lighten-3">
              Eliminar candidato.
            </v-card-title>

            <v-card-text>
              ¿Está seguro de que desea eliminar el candidato? Una vez confirme
              se habrán eliminado los datos del candidato.
            </v-card-text>

            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" text @click="dialogDelete = false">
                Cancelar
              </v-btn>
              <v-btn
                color="primary"
                text
                @click="(dialogDelete = false), deleteElement()"
              >
                Eliminar
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
    <!-- <v-img :src="imageProp()"> </v-img> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      dialogm1: "",
      dialog: false,
      valid: true,
      nombre: "",
      edad: "",
      profesion: "",
      perfil: "",
      educacion: "",
      cargos: "",
      sigep: "",
      imagen: "",
      ir: "",
      partido: "",
      partidoRules: [(v) => !!v || "Se requiere poner un campo en partido"],
      email: "",
      btnSave: "",
      idKey: "",
      selectedImage: null,
      dialogDelete: false,
      validImage: false,
      imageURL: "",
      headers: [
        {
          text: "Nombre",
          align: "start",
          sortable: false,
          value: "nombre",
        },
        { text: "Edad", value: "edad" },
        { text: "Partido", value: "partido" },
        { text: "Profesión", value: "profesion" },
        { text: "Perfil", value: "perfil" },
        { text: "Educación", value: "educacion" },
        { text: "Posiciones", value: "cargos" },
        { text: "Sigep", value: "sigep" },
        { text: "Imagen", value: "imgg" },
        { text: "IR", value: "imgResumen" },
        { text: "Editar", value: "actionsE" },
        { text: "Eliminar", value: "actionsRe" },
      ],
      candidates: [],
    };
  },
  methods: {
    async validate() {
      console.log(this.btnSave);
      if (
        this.$refs.nombre.value !== "" &&
        this.$refs.edad.value !== "" &&
        this.$refs.profesion.value !== "" &&
        this.$refs.partido.value !== "" &&
        this.$refs.perfil.value !== "" &&
        this.$refs.educacion.value !== "" &&
        this.$refs.cargos.value !== "" &&
        this.$refs.sigep.value !== "" &&
        this.$refs.imagen.value !== "" &&
        this.validImage
      ) {
        const axios = require("axios");
        if (this.btnSave === "addMode") {
          console.log("En modo agregar...");
          await axios({
            method: "post",
            url: "https://electorbackend.herokuapp.com/candidatoAdmin",
            data: {
              nombre: `${this.$refs.nombre.value}`,
              edad: `${this.$refs.edad.value}`,
              partido: `${this.$refs.partido.value}`,
              profesion: `${this.$refs.profesion.value}`,
              perfil: `${this.$refs.perfil.value}`,
              educacion: `${this.$refs.educacion.value}`,
              cargos: `${this.$refs.cargos.value}`,
              img: `${this.imageURL}`,
              imgResumen: `${this.selectedImage}`,
              sigep: `${this.$refs.sigep.value}`,
            },
          });
          this.showCadidates();
        } else if (this.btnSave === "editMode") {
          console.log(`this.$refs.nombre.value`);
          await axios({
            method: "put",
            url: `https://electorbackend.herokuapp.com/${this.idKey}`,
            data: {
              nombre: `${this.$refs.nombre.value}`,
              edad: `${this.$refs.edad.value}`,
              partido: `${this.$refs.partido.value}`,
              profesion: `${this.$refs.profesion.value}`,
              perfil: `${this.$refs.perfil.value}`,
              educacion: `${this.$refs.educacion.value}`,
              cargos: `${this.$refs.cargos.value}`,
              img: `${this.imageURL}`,
              imgResumen: `${this.$refs.ir.value}`,
              sigep: `${this.$refs.sigep.value}`,
            },
          }).catch(function (error) {
            // handle error
            console.log(error);
          });
          this.showCadidates();
        }
      } else console.log("No se paso la validacion");
      this.$refs.forCandidate.valid = false;
    },
    async validatePicture(event) {
      console.log(event);

      if (event[0].name !== "") {
        const fileReader = new FileReader();
        fileReader.readAsDataURL(event[0]);
        fileReader.addEventListener("load", () => {
          this.imageURL = fileReader.result;
          console.log(this.imageURL);
          this.validImage = true;
        });

        // this.selectedImage = event[0];
        // this.selectedImage = URL.createObjectURL(event[0]);
        // this.validImage = true;
        console.log("Se pasó la validación de imagen...");
        console.log(this.selectedImage);
      }
    },
    async showCadidates() {
      console.log(this.candidates);
      if (this.candidates) {
        this.candidates = [];
      }
      let candidates = this.candidates;
      console.log("Metodo showCandi");
      const axioss = require("axios");
      await axioss
        .get("https://electorbackend.herokuapp.com/candidatoAdmin")
        .then(function (response) {
          // handle success
          console.log(response.data);
          response.data.forEach((candidate) => {
            candidates.push(candidate);
          });
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        });
    },
    edit(itemID) {
      const listCandidates = this.candidates;
      this.btnSave = "editMode";
      console.log(itemID);
      console.log(this.$refs.dialogForm);
      this.btnSave.onclick;
      const candidaTe = listCandidates.find(
        (candidate) => candidate._id === itemID
      );
      console.log(candidaTe);

      this.nombre = candidaTe.nombre;
      this.edad = candidaTe.edad;
      this.partido = candidaTe.partido;
      this.profesion = candidaTe.profesion;
      this.perfil = candidaTe.perfil;
      this.educacion = candidaTe.educacion;
      this.cargos = candidaTe.cargos;
      this.sigep = candidaTe.sigep;
      this.imagen = candidaTe.img;
      this.ir = candidaTe.imgResumen;
      console.log(this.$refs.nombre);
    },
    addModeButton() {
      this.btnSave = "addMode";
    },
    async deleteElement() {
      console.log(this.idKey);

      const axios = require("axios");

      await axios({
        method: "delete",
        url: `https://electorbackend.herokuapp.com/candidatoAdmin/${this.idKey}`,
      }).catch(function (error) {
        // handle error
        console.log(error);
      });
      this.showCadidates();
    },
    activateDelete() {
      this.dialogDelete = true;
    },
    clearForm() {
      this.nombre = "";
      this.edad = "";
      this.partido = "";
      this.profesion = "";
      this.perfil = "";
      this.educacion = "";
      this.cargos = "";
      this.imagen = "";
      this.ir = null;
      this.sigep = "";
    },
    imageProp() {
      if (this.imageURL === "") {
        return "https://cdn.vuetifyjs.com/images/parallax/material.jpg";
      }

      return this.imageURL;
    },
  },
  computed: {},
  mounted() {
    window.addEventListener("load", () => {
      this.showCadidates();
    });
  },
};
</script>