<template>
  <section>
    <h1>Planets</h1>
    <ul v-if="this.planets !== null" class="list-block">
      <nuxt-link v-for="(planet, index) in this.planets.results" :key="index" class="list-item" no-prefetch active-class="active" :to="/planets/ + planet.url.split('/')[5]">
        {{planet.name}}
      </nuxt-link>
    </ul>
    <div v-if="fetching">
      <Spinner/>
    </div>
    <show-more-btn @showMore="fetchMorePlanets" v-if="!fetching"/>
  </section>
</template>
<script>
  import ShowMoreBtn from "@/components/ShowMoreBtn";
  import Spinner from "@/components/Spinner";
  export default {
    components: {ShowMoreBtn, Spinner},
    // Обработка даты на сервере
    async asyncData({$axios}){
      const planets = await $axios.$get('https://swapi.dev/api/planets')
      return {planets}
    },
    data(){
      return{
        fetching: false,
        page: 1,
        planets: []
      }
    },
    methods: {
      async fetchMorePlanets(){
        this.fetching = true
        this.page++
        const newPlanets = await this.$axios.$get('https://swapi.dev/api/planets?page=' + this.page)
        this.planets.results.push(...newPlanets.results)
        this.fetching = false
      }
    }
  }
</script>
