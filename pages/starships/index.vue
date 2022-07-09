<template>
  <section>
    <h1>Starships</h1>
    <ul v-if="this.starships !== null" class="list-block">
      <nuxt-link v-for="(starship, index) in this.starships.results" :key="index" class="list-item" no-prefetch active-class="active" :to="/starships/ + starship.url.split('/')[5]">
        {{starship.name}}
      </nuxt-link>
    </ul>
  </section>
</template>
<script>
  export default {
    // Обработка даты на сервере
    async asyncData({$axios}){
      const starships = await $axios.$get('https://swapi.dev/api/starships')
      return {starships}
    },
    data(){
      return{
        page: 1,
        starships: []
      }
    },
  }
</script>
