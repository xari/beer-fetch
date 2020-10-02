<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
      style="overflow: clip"
    >
      <div class="d-flex align-center">
        <v-img
          alt="Beer icons"
          class="shrink mr-2"
          contain
          src="https://i.pinimg.com/originals/fb/3b/18/fb3b18e24ef744596f1018fd31ddae5b.png"
          transition="scale-transition"
          width="100"
        />

        <h1>BeerFetch</h1>
      </div>
    </v-app-bar>

    <v-main>
      <Beer/>
    </v-main>
  </v-app>
</template>

<script>
import Beer from './components/Beer';

export default {
  name: 'App',

  components: {
    Beer,
  },

  data: () => ({
    //
  }),
};
</script>
