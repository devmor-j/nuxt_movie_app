<script>
export default {
  name: 'HeroHeader',
  data() {
    return {
      movies: [],
    }
  },

  async fetch() {
    const _ctx = this.$nuxt.context;

    this.movies = await _ctx.$axios.$get('https://jsonplaceholder.typicode.com/todos/1');
  }
}
</script>

<template>
  <v-row>
    <v-col>
      <v-container>
        {{ movies }}
      </v-container>
    </v-col>
  </v-row>
</template>

<style>
</style>
