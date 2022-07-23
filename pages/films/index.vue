<template>
  <section>
    <h1>FILMS</h1>
    <ul class="list-block">
        <nuxt-link
          class="list-item" no-prefetch active-class="active"
          v-for="(film, index) in this.films.results" :key="index"
          :to="/films/ + film.url.split('/')[5]"
        >
          {{film.title}}
        </nuxt-link>
    </ul>
  </section>
</template>
<script>
  export default {
    async asyncData({$axios}){
      const films = await $axios.$get('https://swapi.dev/api/films')
      return {films}
    },
    data(){
      return{
        films: [],
      }
    }
  }
</script>
