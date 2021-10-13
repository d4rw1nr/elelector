<template>
  <div>
    <h1
      class="text-center"
      style="font-family: 'Playfair Display SC', serif; font-size: 3rem"
    >
      Candidatos a la presidencia:
    </h1>
    <h1
      class="text-center mb-9"
      style="font-family: 'Playfair Display SC', serif; font-size: 3rem"
    >
      Sus perfiles partículares
    </h1>
    <v-timeline
      :dense="$vuetify.breakpoint.smAndDown"
      v-model="lineaTiempo"
      :key="timeLineKey"
    >
      <div v-for="(item, index) in listaCandidatos" :key="index" ref="forDiv">
        <div v-if="index % 2 === 0">
          <v-chip class="ma-2" v-model="chipIndex">
            {{ index }}
          </v-chip>
          <candidate-timeline
            class="mb-10 mt-10"
            :nombreCand="propNombre(index)"
            :partidoCand="propPartido(index)"
            :profesionCand="propProfesion(index)"
            :edadCand="propEdad(index)"
            :perfilCand="propPerfil(index)"
            :educacionCand="propEducacion(index)"
            :posicionesCand="propPosiciones(index)"
            :sigepCand="propSigep(index)"
            :imageURLprop="propImg(index)"
          />
        </div>
        <div v-if="index % 2 !== 0">
          <candidate-timeline-2
            :nombreCand="propNombre(index)"
            :partidoCand="propPartido(index)"
            :profesionCand="propProfesion(index)"
            :edadCand="propEdad(index)"
            :perfilCand="propPerfil(index)"
            :educacionCand="propEducacion(index)"
            :posicionesCand="propPosiciones(index)"
            :sigepCand="propSigep(index)"
            :imageURLprop="propImg(index)"
          />
        </div>
      </div>
    </v-timeline>
  </div>
</template>



<script>
import CandidateTimeline from "../components/CandidateTimeline.vue";
import CandidateTimeline2 from "../components/CandidateTimeline2.vue";

export default {
  components: {
    CandidateTimeline,
    CandidateTimeline2,
  },
  methods: {
    async showCadidates() {
      this.listaCandidatos = [];
      let listaCandidatos = this.listaCandidatos;

      const axios = require("axios");
      await axios
        .get("https://electorbackend.herokuapp.com/candidatoAdmin")
        .then(function (response) {
          // handle success
          console.log(response.data[0].nombre);
          response.data.forEach(async (candidate) => {
            await listaCandidatos.push(candidate);
          });
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        });
    },
    propNombre(index) {
      if (this.listaCandidatos[0] === undefined) {
        console.log(this.index);
        return "Se necesita recargar para mostrar los datos: F5.";
      }
      console.log(this.listaCandidatos[index]);
      return this.listaCandidatos[index].nombre;
    },
    propPartido(index) {
      if (this.listaCandidatos[0] === undefined) {
        console.log(this.index);
        return "Se necesita recargar para mostrar los datos: F5.";
      }
      console.log(this.listaCandidatos[index].partido);
      return this.listaCandidatos[index].partido;
    },
    propProfesion(index) {
      if (this.listaCandidatos[0] === undefined) {
        return "Se necesita recargar para mostrar los datos: F5.";
      }
      console.log(this.listaCandidatos[index].profesion);
      return this.listaCandidatos[index].profesion;
    },
    propEdad(index) {
      if (this.listaCandidatos[0] === undefined) {
        return "Se necesita recargar para mostrar los datos: F5.";
      }
      console.log(this.listaCandidatos[index].edad);
      return this.listaCandidatos[index].edad;
    },
    propPerfil(index) {
      if (this.listaCandidatos[0] === undefined) {
        return "Se necesita recargar para mostrar los datos: F5.";
      }
      console.log(this.listaCandidatos[index].perfil);
      return this.listaCandidatos[index].perfil;
    },
    propEducacion(index) {
      if (this.listaCandidatos[0] === undefined) {
        return "Se necesita recargar para mostrar los datos: F5.";
      }
      console.log(this.listaCandidatos[index].educacion);
      return this.listaCandidatos[index].educacion;
    },
    propEducacion(index) {
      if (this.listaCandidatos[0] === undefined) {
        return "Se necesita recargar para mostrar los datos: F5.";
      }
      console.log(this.listaCandidatos[index].educacion);
      return this.listaCandidatos[index].educacion;
    },
    propPosiciones(index) {
      if (this.listaCandidatos[0] === undefined) {
        return "Se necesita recargar para mostrar los datos: F5.";
      }
      console.log(this.listaCandidatos[index].cargos);
      return this.listaCandidatos[index].cargos;
    },
    propSigep(index) {
      if (this.listaCandidatos[0] === undefined) {
        return "Se necesita recargar para mostrar los datos: F5.";
      }
      console.log(this.listaCandidatos[index].sigep);
      return this.listaCandidatos[index].sigep;
    },
    propImg(index) {
      if (this.listaCandidatos[0] === undefined) {
        return;
      }
      console.log(this.listaCandidatos[index].img);
      return this.listaCandidatos[index].img;
    },
  },
  data: () => ({
    listaCandidatos: [],
    lineaTiempo: "",
    timeLineKey: 0,
    index: 0,
    chipIndex: 0,
  }),
  computed: {},
  mounted() {
    window.addEventListener("load", () => {
      this.showCadidates();
    });
  },
  watch: {},
};
</script>

<style scoped>
.backGround {
  background-color: rgb(0, 0, 0);
  color: white;
}
</style>