<template>
  <section v-if="starships !== null && !loading">
    <div class="user-block">
      <div>
        <p class="title">Starship Model: {{this.starships.name}}</p>
        <p>cargo_capacity: {{this.starships.cargo_capacity}}</p>
        <p>consumables: {{this.starships.consumables}}</p>
        <p>cost_in_credits: {{this.starships.cost_in_credits}}</p>
        <p>crew: {{this.starships.crew}}</p>
        <p>hyperdrive_rating: {{this.starships.hyperdrive_rating}}</p>
        <p>length: {{this.starships.length}}</p>
        <p>manufacturer: {{this.starships.manufacturer}}</p>
        <p>max_atmosphering_speed: {{this.starships.max_atmosphering_speed}}</p>
        <p>passengers: {{this.starships.passengers}}</p>
      </div>
    </div>
    <div v-if="this.films.length > 0">
      <h1>This Starship in films1</h1>
      <ul class="list-block">
        <nuxt-link v-for="film in this.films" :key="index" class="list-item" no-prefetch active-class="active" :to="/films/ + film.url.split('/')[5]">
          {{film.title}}
        </nuxt-link>
      </ul>
    </div>
    <div v-if="this.pilots.length > 0">
      <h1>Pilots of this Starship</h1>
      <ul class="list-block">
        <nuxt-link v-for="pilot in this.pilots" :key="index" class="list-item" no-prefetch active-class="active" :to="/users/ + pilot.url.split('/')[5]">
          {{pilot.name}}
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
        starships: [],
        films: [],
        pilots: [],
        loading: true
      }
    },
    validate({params}){
      return /^\d+$/.test(params.id)
    },
    async mounted() {
      this.starships = await this.$axios.$get('https://swapi.dev/api/starships/' + this.$route.params.id)

      for(let i = 0; i < this.starships.films.length; i++){
        this.films.push(await this.$axios.$get(this.starships.films[i]))
      }

      for(let i = 0; i < this.starships.pilots.length; i++){
        this.pilots.push(await this.$axios.$get(this.starships.pilots[i]))
      }

      this.loading=false
    },
  }
</script>

<style scoped lang="scss">
  .title{
    font-size: 22px;
    font-weight: bold;
  }
</style>
