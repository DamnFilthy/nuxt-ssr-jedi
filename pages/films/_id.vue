<template>
  <section v-if="this.films !== null && !loading">
    <div class="user-block">
      <div v-if="this.films">
        <p class="title">Title: {{this.films.title}}</p>
        <p>Opening Crawl: {{this.films.opening_crawl}}</p>
        <p>Director: {{this.films.director}}</p>
        <p>Producer: {{this.films.producer}}</p>
        <p>Release Date: {{this.films.release_date}}</p>
      </div>
    </div>
    <div>
      <h1>Characters in this film</h1>
      <ul v-if="this.nameResidents.length > 0" class="list-block">
        <nuxt-link v-for="resident in this.nameResidents" :key="index" class="list-item" no-prefetch
                   active-class="active" :to="/users/ + resident.url.split('/')[5]">
          {{resident.name}}
        </nuxt-link>
      </ul>
      <div v-else>No data...</div>
    </div>
    <div>
      <h1>Planets in this film</h1>
      <ul v-if="this.planetsInFilm.length > 0" class="list-block">
        <nuxt-link v-for="planet in this.planetsInFilm" :key="index" class="list-item" no-prefetch active-class="active"
                   :to="/planets/ + planet.url.split('/')[5]">
          {{planet.name}}
        </nuxt-link>
      </ul>
      <div v-else>No data...</div>
    </div>
    <div>
      <h1>starships in this film</h1>
      <ul v-if="this.starships.length > 0" class="list-block">
        <nuxt-link v-for="starship in this.starships" :key="index" class="list-item" no-prefetch active-class="active"
                   :to="/starships/ + starship.url.split('/')[5]">
          {{starship.name}}
        </nuxt-link>
      </ul>
      <div v-else>No data...</div>
    </div>
    <div>
      <h1>species in this film</h1>
      <ul v-if="this.species.length > 0" class="list-block">
        <nuxt-link v-for="specie in this.planetsInFilm" :key="index" class="list-item" no-prefetch active-class="active"
                   :to="/species/ + specie.url.split('/')[5]">
          {{specie.name}}
        </nuxt-link>
      </ul>
      <div v-else>No data...</div>
    </div>
  </section>
  <section v-else-if="loading" class="loading-page">
    <Spinner/>
  </section>
</template>

<script>
  import Spinner from "@/components/Spinner"

  export default {
    components: {Spinner},
    data() {
      return {
        films: [],
        nameResidents: [],
        planetsInFilm: [],
        starships: [],
        species: [],
        loading: true
      }
    },
    validate({params}) {
      return /^\d+$/.test(params.id)
    },
    async mounted() {
      this.films = await this.$axios.$get('https://swapi.dev/api/films/' + this.$route.params.id)

      for (let i = 0; i < this.films.characters.length; i++) {
        this.nameResidents.push(await this.$axios.$get(this.films.characters[i]))
      }

      for (let i = 0; i < this.films.planets.length; i++) {
        this.planetsInFilm.push(await this.$axios.$get(this.films.planets[i]))
      }

      for (let i = 0; i < this.films.starships.length; i++) {
        this.starships.push(await this.$axios.$get(this.films.starships[i]))
      }

      for (let i = 0; i < this.films.species.length; i++) {
        this.species.push(await this.$axios.$get(this.films.species[i]))
      }

      this.loading = false
    },
  }
</script>

<style scoped lang="scss">
  .title {
    font-size: 22px;
    font-weight: bold;
  }
</style>
