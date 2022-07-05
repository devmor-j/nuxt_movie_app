<script>
export default {
  data() {
    return {
      movie: {},
    }
  },

  async fetch() {
    this.movie = await JSON.parse(this.$nuxt.context.params.movie)
  }
}
</script>

<template>
  <v-row class="justify-sm-center">
    <v-col>
      <v-container>
        <v-row justify="center" align="start">

          <v-col sm="6">
            <v-img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`">
            </v-img>
          </v-col>

          <v-col sm="6">
            <h1 class="break-word">
              {{ movie.title }}
            </h1>
            <h2 v-if="movie.title !== movie.original_title" class="break-word">
              {{ movie.original_title }}
            </h2>

            <time class="grey--text" :datetime="new Date(movie.release_date)">
              {{ new Date(movie.release_date).toLocaleDateString('default', {
                  day: 'numeric',
                  month: 'long',
                  year: "numeric"
                })
              }}
            </time>

            <p class="my-6">
              {{ movie.overview }}
            </p>

            <v-chip-group column class="my-4">
              <v-chip :class="movie.vote_count < 1000 ? 'red--text' : 'grey--text'" outlined label>
                <v-icon small left>
                  mdi-vote
                </v-icon>
                Votes:&nbsp;
                <span class="font-weight-bold">{{ movie.vote_count }}</span>
              </v-chip>

              <v-chip
                :class="movie.vote_average > 7.5 ? 'green--text' : (movie.vote_average < 5 ? 'red--text' : 'grey--text')"
                outlined label>
                <v-icon small left>
                  mdi-star
                </v-icon>
                Rating:&nbsp;
                <span class="font-weight-bold">{{ movie.vote_average }}</span>
              </v-chip>

              <v-chip :class="movie.original_language !== 'en' ? 'red--text' : 'grey--text'" outlined label>
                <v-icon small left>
                  mdi-earth
                </v-icon>
                Language:&nbsp;
                <span class="font-weight-bold text-uppercase">{{ movie.original_language }}</span>
              </v-chip>
            </v-chip-group>

          </v-col>
        </v-row>
      </v-container>
    </v-col>
  </v-row>
</template>