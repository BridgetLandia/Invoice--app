<template>
  <v-app>
    <invoice />
  </v-app>
</template>

<script>
import Invoice from "./components/Invoice";

export default {
  name: "App",

  components: {
    Invoice,
  },

  data: () => ({
    //
  }),
};
</script>
