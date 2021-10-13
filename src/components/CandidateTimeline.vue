<template>
  <v-lazy
    class="mt-5"
    v-model="isActive"
    :options="{
      threshold: 0.9,
    }"
    min-height="200"
    dark
  >
    <transition name="myTransition">
      <v-timeline-item v-if="isActive" color="#858488">
        <v-img
          slot="opposite"
          :src="renderImage()"
          max-height="100em"
          max-width="500"
          class="mx-auto"
          v-model="opposite"
        ></v-img>
        <v-card class="elevation-0">
          <v-card-title class="text-h5">
            <h1
              style="font-family: 'Playfair Display SC', serif; font-size: 3rem"
              class="mb-6"
            >
              {{ nombreCand }}
            </h1>
          </v-card-title>
          <v-card-text>
            <ul>
              <li
                style="font-family: 'Monserat', serif; font-size: 1.5rem"
                class="mb-2"
              >
                <strong>Partido: </strong>{{ partidoCand }}
              </li>
              <li
                style="font-family: 'Monserat', serif; font-size: 1.5rem"
                class="mb-2"
              >
                <strong>Profesión: </strong>{{ profesionCand }}
              </li>
              <li
                style="font-family: 'Monserat', serif; font-size: 1.5rem"
                class="mb-2"
              >
                <strong>Edad: </strong>{{ edadCand }}
              </li>
              <li
                style="font-family: 'Monserat', serif; font-size: 1.5rem"
                class="mb-2"
              >
                <strong>Perfil: </strong>{{ perfilCand }}
              </li>
              <li
                style="font-family: 'Monserat', serif; font-size: 1.5rem"
                class="mb-2"
              >
                <strong>Educación: </strong>{{ educacionCand }}
              </li>
              <li
                style="font-family: 'Monserat', serif; font-size: 1.5rem"
                class="mb-2"
              >
                <strong>Cargos: </strong>{{ posicionesCand }}
              </li>
              <li
                style="font-family: 'Monserat', serif; font-size: 1.5rem"
                class="mb-2"
              >
                <strong>Sigep: </strong>{{ sigepCand }}
              </li>
            </ul>
          </v-card-text>
        </v-card>
      </v-timeline-item>
    </transition>
  </v-lazy>
</template>

<script>
export default {
  name: "CandidateTimeline",
  data: () => ({
    isActive: false,
    image: "",
    reversee: true,
    opposite: "",
    imageURL: "",
  }),
  props: {
    partidoCand: {
      default: " Partido del candidato",
    },
    reverse: {
      type: String,
      default: "opposite",
    },
    nombreCand: {
      type: String,
      default: "Nombre del candidato",
    },
    profesionCand: {
      type: String,
      default: "Profesión del candidato",
    },
    edadCand: {
      type: String,
      default: "Edad del candidato",
    },
    perfilCand: {
      type: String,
      default: "Perfil del candidato",
    },
    educacionCand: {
      type: String,
      default: "Educación del candidato",
    },
    posicionesCand: {
      type: String,
      default: "Posiciones anteriores del candidato",
    },
    sigepCand: {
      type: String,
      default: "Sigep del candidato",
    },
    imageURLprop: {
      type: String,
      default:
        "https://e7.pngegg.com/pngimages/691/765/png-clipart-primary-profile-illustration-computer-icons-person-anonymous-miscellaneous-silhouette.png",
    },
  },
  methods: {
    renderImage() {
      return this.imageURLprop;
    },
  },
};
</script>

<style scoped>
.myTransition-enter-active,
.myTransition-leave-active {
  transition: opacity 2.5s;
}
.myTransition-enter,
.myTransition-leave-to {
  opacity: 0;
}

.bodyTextCand-style {
  font-family: "Alegreya", serif;
  font-size: 3rem;
}
</style>