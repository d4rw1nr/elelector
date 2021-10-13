<template>
  <div>
    <v-app>
      <v-carousel reverse-transition="fade-transition" transition="fade-transition">
        <v-carousel-item
        v-for="(candidato, index) in candidatos"
        :key="index"
        @click="getCandidato()">
              <v-card
              width="100%"
              height="100%"
              :img="candidato.imagen" contain>
                      <v-container>
                      <v-row>
                        <v-col cols="12" md="7" lg="7">
                          <br><br><br>
                          <h1 id="titulo">{{candidato.nombre}}</h1>
                          <h2 id="subtitulo">{{candidato.partido}}</h2>
                          <h3 id="texto">{{candidato.perfil}}</h3>
                        </v-col>
                      </v-row>
                      </v-container>
              </v-card>
        </v-carousel-item>
      </v-carousel>
    </v-app>
  </div>
</template>

<script>
export default {
  name: "CarouselCandidate",
  data() {
    return {
      candidatos: [
        {
          nombre: "Gustavo Petro",
          partido: "Movimiento Colombia Humana",
          perfil: "Político y economista fundador de la Colombia humana",
          imagen: require('@/assets/petro.jpg'),
        },
        {
          nombre: "Óscar Iván Zuluaga",
          partido: "Partido Centro Democrático",
          perfil: "Economista, empresario y político colombiano",
          imagen: require('@/assets/zuluaga.jpg'),
        },
        {
          nombre: "Alejandro Gaviria",
          partido: "Partido Liberal Colombiano",
          perfil: "Académico, economista, escritor, ingeniero y político colombiano nacido en Chile",
          imagen: require('@/assets/gaviria.jpg'),
        },
        {
          nombre: "María Fernanda Cabal",
          partido: "Partido Centro Democrático",
          perfil: "Empresaria, politóloga y política minarquista colombiana",
          imagen: require('@/assets/cabal.jpg'),
        },
        {
          nombre: "Sergio Fajardo Valderrama",
          partido: "Partido Alianza Verde",
          perfil: "Matemático, exalcalde de Medellín y exgobernador de Antioquia",
          imagen: require('@/assets/fajardo.jpg'),
        },
        {
          nombre: "Federico Andrés Gutiérrez",
          partido: "Partido Liberal Colombiano",
          perfil: "Ingeniero civil y político colombiano",
          imagen: require('@/assets/federico.jpg'),
        },
      ],
    };
  },
  
  methods: {
    getCandidato() {
      this.$router.push("Candidato");
    },
  },
}

</script>

<style>

#titulo{
  font-size: 4rem;
  text-shadow: 1px 1px 0px white;
}
#subtitulo{
  font-size: 2rem;
  text-shadow: 1px 1px 0px white;
}
#texto{
  font-size: 1.5rem;
  text-shadow: 1px 1px 0px white;
}

</style>