<template>
  <section>
    <h1>Species</h1>
    <ul v-if="this.species !== null" class="list-block">
      <nuxt-link v-for="(specie, index) in this.species.results" :key="index" class="list-item" no-prefetch active-class="active" :to="/species/ + specie.url.split('/')[5]">
        {{specie.name}}
      </nuxt-link>
    </ul>
  </section>
</template>
<script>
  export default {
    // Обработка даты на сервере
    async asyncData({$axios}){
      const species = await $axios.$get('https://swapi.dev/api/species')
      return {species}
    },
    data(){
      return{
        page: 1,
        starships: []
      }
    },
  }
</script>
