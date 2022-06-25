<script>
export default {
  name: 'HeroHeader',
  data() {
    return {
      popularMovies: [],
      upcomingMovies: [],
      show: false,
    }
  },

  async fetch() {
    const ctx = this.$nuxt.context;

    const popularMoviesUrl = `${ctx.$config.baseUrl}/movie/popular?api_key=${ctx.$config.apiKey}`;
    const upcomingMoviesUrl = `${ctx.$config.baseUrl}/movie/upcoming?api_key=${ctx.$config.apiKey}`;

    const get = async (fullUrl) => await ctx.$axios.$get(fullUrl)

    await Promise.allSettled([
      get(popularMoviesUrl),
      get(upcomingMoviesUrl)
    ])
      .then((data) => {
        this.popularMovies = data[0].value.results;
        this.upcomingMovies = data[1].value.results;
      });
  }
}
</script>

<template>
  <v-row class="justify-sm-center">
    <v-col>
      <v-container>
        <v-row justify="center" align="start">
          <v-card v-for="movie in popularMovies" :key="movie.id" :max-width="500" width="100%" class="rounded ma-4">
            <v-img :src="`https://image.tmdb.org/t/p/w500${movie.backdrop_path}`">
              <div class="d-flex flex-column pa-2 align-start">
                <small title="Vote Count">
                  <v-icon small left>mdi-vote</v-icon> {{ movie.vote_count }}
                </small>
                <small title="Vote Average">
                  <v-icon small left>mdi-star</v-icon> {{ movie.vote_average }}
                </small>
                <small class="text-uppercase" title="Language">
                  <v-icon small left>mdi-earth</v-icon> {{ movie.original_language }}
                </small>
              </div>
            </v-img>
            <v-card-title class="break-word">{{ movie.title }} <span v-if="movie.title !== movie.original_title">{{
                movie.original_title
            }}</span></v-card-title>
            <v-card-subtitle>
              {{ new Date(movie.release_date).toLocaleDateString('default', {
                  day: 'numeric',
                  month: 'long',
                  year: "numeric"
                })
              }} </v-card-subtitle>
            <v-card-text>
              {{ movie.overview }}
            </v-card-text>
            <v-card-actions>
              <v-btn class="purple--text" text outlined>Read More</v-btn>
              <!-- <v-spacer></v-spacer> -->
              <!-- <v-btn icon @click="show = !show">
              <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
            </v-btn> -->
            </v-card-actions>
            <!-- <v-expand-transition>
            <div v-show="show">
              <v-divider></v-divider>
              <v-list>
                <v-list-item>4K 10.81GB</v-list-item>
                <v-list-item>1080p 2.56GB</v-list-item>
                <v-list-item>720p 1.23GB</v-list-item>
                <v-list-item>480p 0.76GB</v-list-item>
              </v-list>
            </div>
          </v-expand-transition> -->
          </v-card>
        </v-row>
      </v-container>
    </v-col>
  </v-row>
</template>

<style scoped>
.break-word {
  word-break: break-word;
}

small[title] {
  user-select: none;
  background-color: rgb(0 0 0 / 0.25);
  padding-inline: 0.25rem;
  margin-block: 0.125rem;
  border-radius: 0.125rem;
  min-width: 10ch;
}
</style>
