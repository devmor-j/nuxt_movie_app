<script>
export default {
  name: 'HeroHeader',
}
</script>

<template>
  <v-row class="background-image" align="end">
    <!-- <v-switch hint="Theme" dense hide-details="auto" v-model="$vuetify.theme.dark" -->
      <!-- :label="$vuetify.theme.dark ? 'Dark' : 'Light'"></v-switch> -->
    <v-col class="px-0">
      <v-container>
        <h2 class="text-h2 pb-4">Now Streaming</h2>
        <v-btn class="secondary--text" text outlined>Explore</v-btn>
      </v-container>
    </v-col>
  </v-row>
</template>

<style scoped>
.background-image {
  background-image: linear-gradient(to top, rgb(0 0 0 / 0.5), transparent), url("/images/popcorn.jpg");
  min-height: 35vh;
  background-repeat: no-repeat;
  background-position: 50% 30%;
  background-size: cover;
}
</style>
