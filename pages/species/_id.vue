<template>
  <section v-if="!loading">
    <h1>{{this.species.name}}</h1>
    <div class="user-block">
      <div>
        <p>average_height: {{this.species.average_height}}</p>
        <p>average_lifespan: {{this.species.average_lifespan}}</p>
        <p>classification: {{this.species.classification}}</p>
        <p>designation: {{this.species.designation}}</p>
        <p>eye_colors: {{this.species.eye_colors}}</p>
        <p>hair_colors: {{this.species.hair_colors}}</p>
        <p>language: {{this.species.language}}</p>
      </div>
    </div>
    <div v-if="this.homeworld !== null">
      <h1>Homeworld</h1>
      <ul class="list-block">
        <nuxt-link class="list-item" no-prefetch active-class="active"
                   :to="'/planets/' + this.homeworld.url.split('/')[5]">
          HomeWorld: {{this.homeworld.name}}
        </nuxt-link>
      </ul>
    </div>
    <div>
      <h1>Characters this type</h1>
      <ul v-if="this.people" class="list-block">
        <nuxt-link v-for="man in this.people" :key="index" class="list-item" no-prefetch active-class="active"
                   :to="/users/ + man.url.split('/')[5]">
          {{man.name}}
        </nuxt-link>
      </ul>
    </div>
    <div>
      <h1>This types in films1</h1>
      <ul v-if="this.films" class="list-block">
        <nuxt-link v-for="film in this.films" :key="index" class="list-item" no-prefetch active-class="active"
                   :to="/films/ + film.url.split('/')[5]">
          {{film.title}}
        </nuxt-link>
      </ul>
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
        species: [],
        films: [],
        people: [],
        homeworld: null,
        loading: true
      }
    },
    validate({params}) {
      return /^\d+$/.test(params.id)
    },
    async mounted() {
      this.species = await this.$axios.$get('https://swapi.dev/api/species/' + this.$route.params.id)

      for (let i = 0; i < this.species.films.length; i++) {
        this.films.push(await this.$axios.$get(this.species.films[i]))
      }

      for (let i = 0; i < this.species.people.length; i++) {
        this.people.push(await this.$axios.$get(this.species.people[i]))
      }

      if (this.species.homeworld) {
        this.homeworld = await this.$axios.$get(this.species.homeworld)
      } else {
        this.homeworld = null
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
