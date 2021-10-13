<template>
  <v-app>
    <v-btn block x-large>
      <v-app-bar app flat extended>
        <v-spacer></v-spacer>
        <v-app-bar-title
          ><h1
            @click="getHome"
            style="font-family: 'Playfair Display SC', serif; font-size: 5rem"
          >
            El Elector
          </h1></v-app-bar-title
        >
        <v-spacer></v-spacer>
      </v-app-bar>
    </v-btn>

    <v-main>
      <router-view />
    </v-main>

    <v-footer dark padless>
      <v-card class="flex" flat tile>
        <!-- CREAR GRILLA DE CONTENIDO -->
        <v-card-text class="py-2 white--text text-center">
          {{ new Date().getFullYear() }} — <strong>@elector </strong>
        </v-card-text>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
  methods: {
    getHome() {
      this.$router.push("/");
    },
  },
};
</script>
