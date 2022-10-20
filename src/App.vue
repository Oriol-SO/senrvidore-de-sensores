<template>
  <v-app>
    <v-main>
      <fondo/>
    </v-main>
  </v-app>
</template>

<script>
import fondo from './components/fondo.vue';

export default {
  name: 'App',
  components: {
    fondo,
  },

  data: () => ({
    //
  }),
};
</script>
