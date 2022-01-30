<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center title">
        Minigame :: Fabricio Braga
      </div>

      <v-spacer></v-spacer>

    </v-app-bar>

    <v-main>
      <Game />
    </v-main>
  </v-app>
</template>

<script>

import Game from './components/Game.vue';

export default {
  name: 'App',

  components: {
    Game,
  },

  data: () => ({
    //
  }),
};
</script>
