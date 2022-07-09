<template>
  <section v-if="this.films !== null && !loading">
    <h1>FILMS</h1>
    <ul class="list-block">
        <nuxt-link  v-for="(film, index) in this.films.results" :key="index" class="list-item" no-prefetch active-class="active" :to="/films/ + film.url.split('/')[5]">
          {{film.title}}
        </nuxt-link>
    </ul>
  </section>
  <section v-else-if="loading" class="loading-page">
    <h1>Loading ...</h1>
  </section>
</template>
<script>
  export default {
    data(){
      return{
        page: 1,
        films: null,
        loading: true
      }
    },
    async created() {
       this.films = await this.$axios.$get('https://swapi.dev/api/films')
      this.loading = false
    },
  }
</script>
