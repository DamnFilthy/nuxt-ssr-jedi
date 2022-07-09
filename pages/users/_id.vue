<template>
  <div>
    <section v-if="user !== null && homeworld !== null && !loading">
      <h1>User {{$route.params.id}}</h1>
      <div class="user-block">
        <div>
          <p class="title">Name: {{this.user.name}}</p>
          <p>Height: {{this.user.height}}</p>
          <p>Mass: {{this.user.mass}}</p>
          <p>Hair Color: {{this.user.hair_color}}</p>
          <p>Skin Color: {{this.user.skin_color}}</p>
          <p>Eye Color: {{this.user.eye_color}}</p>
          <p>Birth Year: {{this.user.birth_year}}</p>
          <p>Gender: {{this.user.gender}}</p>
        </div>
        <div>
          <p class="title">HomeWorld: {{this.homeworld.name}}</p>
          <p>Rotation Period: {{this.homeworld.rotation_period}}</p>
          <p>Orbital Perioud: {{this.homeworld.orbital_period}}</p>
          <p>Diameter: {{this.homeworld.diameter}}</p>
          <p>Climate: {{this.homeworld.climate}}</p>
          <p>Gravity: {{this.homeworld.gravity}}</p>
          <p>Terrain: {{this.homeworld.terrain}}</p>
          <p>Surface Water: {{this.homeworld.surface_water}}</p>
          <p>Population: {{this.homeworld.population}}</p>
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
  </div>

</template>

<script>

  export default {
    data(){
      return{
        user: null,
        homeworld: null,
        nameResidents: [],
        loading: true
      }
    },
    validate({params}){
     return /^\d+$/.test(params.id)
    },
    async mounted() {
      this.user = await this.$axios.$get('https://swapi.dev/api/people/' + this.$route.params.id)
      this.homeworld = await this.$axios.$get(this.user.homeworld)

      for(let i = 0; i < this.homeworld.residents.length; i++){
        this.nameResidents.push(await this.$axios.$get(this.homeworld.residents[i]))
      }
      this.loading = false
    },
  }
</script>

<style lang="scss">
  .user-block{
    display: flex;
    justify-content: center;
    align-items: flex-start;
    border: 2px solid wheat;
    padding: 30px;
    div{
      margin-right: 30px;
    }
  }
  .loading-page{
    height: 80vh;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .title{
    font-size: 22px;
    font-weight: bold;
  }
  @media (max-width: 475px){
    .user-block{
      flex-direction: column;
      align-items: center;
    }
  }
</style>
