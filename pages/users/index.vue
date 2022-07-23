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
           <Spinner/>
        </div>
        <show-more-btn @showMore="fetchMorePeople" v-if="!fetching"/>
      </div>
    </section>
    <section v-else-if="loading" class="loading-page">
      <Spinner/>
    </section>
  </div>

</template>
<script>
  import ShowMoreBtn from "@/components/ShowMoreBtn";
  import Spinner from "@/components/Spinner";

  export default {
    components: {ShowMoreBtn, Spinner},
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
