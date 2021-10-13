<template>
  <div>
    <v-layout wrap>
      <v-flex xs12>
        <v-app-bar class="mt-6">
          <v-tabs centered grow color="#BDBDBD">
            <v-tab class="grande">Home</v-tab>
            <v-tab class="grande" @click="getCandidato()">Candidatos</v-tab>
            <v-tab class="grande" @click="getContacto()">Contáctenos</v-tab>
          </v-tabs>
        </v-app-bar>
      </v-flex>
    </v-layout>
    <v-divider></v-divider>

    <v-layout justify-center class="mt-0" wrap>
      <v-flex xs12 md12>
        <v-parallax src="@/assets/background.png" height="700">
          <h1
            class="text-center mt-10 mb-3"
            style="font-family: 'Libre Baskerville', serif; font-size: 3.5rem"
          >
            ¿Quiénes somos?
          </h1>
          <v-layout justify-center wrap>
            <v-flex xs12 md10>
              <h3
                class="text-justify mr-15 ml-15 mb-15"
                style="
                  font-family: 'Gentium Book Basic', serif;
                  font-size: 3rem;
                "
              >
                Somos una plataforma que centraliza la información de candidatos
                a elecciones. Con esta plataforma se busca aportar en la
                necesidad de una central de información verificada que esté
                dispuesta al público y que sea una ayuda para los gobiernos
                democráticos.
              </h3>
            </v-flex>
          </v-layout>
        </v-parallax>
      </v-flex>
    </v-layout>

    <v-divider class="mt-15 grey darken-3"></v-divider>
    <v-divider class="mt-0 grey darken-3"></v-divider>
    <v-divider class="mt-0 grey darken-3"></v-divider>
    <v-divider class="mt-0 grey darken-3"></v-divider>
    <center>
      <h1
        class="mt-5"
        style="
          font-family: 'Libre Baskerville', serif;
          font-size: 3.5rem;
          color: #424242;
        "
      >
        CANDIDATOS
      </h1>
    </center>
    <v-divider class="mt-0 grey darken-3"></v-divider>
    <v-divider class="mt-0 grey darken-3"></v-divider>
    <v-divider class="mt-0 grey darken-3"></v-divider>
    <v-divider class="mt-0 grey darken-3"></v-divider>
    <br>
    <carousel-candidate/>
  </div>
</template>

<script>
import CarouselCandidate from "../components/Carrusel.vue";

export default {
  name: "HelloWorld",

  data: () => ({
    colors: ["primary", "secondary", "yellow darken-2", "red", "orange"],
    colorsNotice: ["secondary", "yellow darken-2", "primary", "orange", "red"],
  }),
  methods: {
    getCandidato() {
      this.$router.push("Candidato");
    },
    getContacto() {
      this.$router.push("Contacto");
    },
    getNotice(notice) {
      var numNoticia = [
        "Noticia politico uno",
        "Noticia politico dos",
        "Noticia politico tres",
        "Noticia politico cuatro",
        "Noticia politico cinco",
      ];
      console.log("link " + numNoticia[notice]);
    },
  },
  components: {
    CarouselCandidate,
  },
};
</script>

<style>

.grande{
  font-size: 1.5rem;
}

</style>
