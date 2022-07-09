<template>
  <section v-if="!loading">
    <div class="user-block">
    <div>
      <p class="title">HomeWorld: {{this.planets.name}}</p>
      <p>Rotation Period: {{this.planets.rotation_period}}</p>
      <p>Orbital Perioud: {{this.planets.orbital_period}}</p>
      <p>Diameter: {{this.planets.diameter}}</p>
      <p>Climate: {{this.planets.climate}}</p>
      <p>Gravity: {{this.planets.gravity}}</p>
      <p>Terrain: {{this.planets.terrain}}</p>
      <p>Surface Water: {{this.planets.surface_water}}</p>
      <p>Population: {{this.planets.population}}</p>
    </div>
    </div>
    <div>
      <h1>Other persons on this planet</h1>
      <ul v-if="this.nameResidents" class="list-block">
        <nuxt-link v-for="resident in this.nameResidents" :key="index" class="list-item" no-prefetch active-class="active" :to="/users/ + resident.url.split('/')[5]">
          {{resident.name}}
        </nuxt-link>
      </ul>
    </div>
  </section>
  <section v-else-if="loading" class="loading-page">
    <h1>Loading ...</h1>
  </section>
</template>

<script>
  export default {
    data(){
      return{
        planets: [],
        nameResidents: [],
        loading: true
      }
    },
    validate({params}){
      return /^\d+$/.test(params.id)
    },
    async mounted() {
      this.planets = await this.$axios.$get('https://swapi.dev/api/planets/' + this.$route.params.id)

      for(let i = 0; i < this.planets.residents.length; i++){
        this.nameResidents.push(await this.$axios.$get(this.planets.residents[i]))
      }

      this.loading = false
    },
  }
</script>

<style scoped lang="scss">
  .title{
    font-size: 22px;
    font-weight: bold;
  }
</style>
