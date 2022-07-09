<template>
  <div>
    <section v-if="!loading">
      <div>
        <h1>Heroes</h1>
        <ul v-if="this.users !== null" class="list-block">
          <nuxt-link v-for="(user, index) in this.users.results" :key="index" class="list-item" no-prefetch active-class="active" :to="/users/ + user.url.split('/')[5]">
            {{user.name}}
          </nuxt-link>
        </ul>
        <div v-if="fetching">
         <h1>Loading ...</h1>
        </div>
        <button @click.prevent="fetchMorePeople">Показать еще</button>
      </div>
    </section>
    <section v-else-if="loading" class="loading-page">
      <h1>Loading ...</h1>
    </section>
  </div>

</template>
<script>
  export default {
    // Обработка даты на сервере
    // async asyncData({$axios}){
    //   const users = await $axios.$get('https://swapi.dev/api/people')
    //   return {users}
    // },
    data(){
      return{
        page: 1,
        users: [],
        loading:false,
        fetching: false,
      }
    },
    async mounted(){
      this.loading = true
      this.users =  await this.$axios.$get('https://swapi.dev/api/people')
      this.loading = false
    },
    methods: {
      async fetchMorePeople(){
        this.fetching = true
        this.page++
        const newUsers = await this.$axios.$get('https://swapi.dev/api/people?page=' + this.page)
        await this.users.results.push(...newUsers.results)
        this.fetching = false
      }
    },
  }
</script>
