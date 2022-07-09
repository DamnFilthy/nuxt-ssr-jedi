<template>
  <section>
    <h1>Planets</h1>
    <ul v-if="this.planets !== null" class="list-block">
      <nuxt-link v-for="(planet, index) in this.planets.results" :key="index" class="list-item" no-prefetch active-class="active" :to="/planets/ + planet.url.split('/')[5]">
        {{planet.name}}
      </nuxt-link>
    </ul>
    <button @click.prevent="fetchMorePlanets">Показать еще</button>
  </section>
</template>
<script>
  export default {
    // Обработка даты на сервере
    async asyncData({$axios}){
      const planets = await $axios.$get('https://swapi.dev/api/planets')
      return {planets}
    },
    data(){
      return{
        page: 1,
        planets: []
      }
    },
    methods: {
      async fetchMorePlanets(){
        this.page++
        const newPlanets = await this.$axios.$get('https://swapi.dev/api/planets?page=' + this.page)
        this.planets.results.push(...newPlanets.results)
      }
    }
  }
</script>
