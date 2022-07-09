<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark" class="my-navbar">
      <nuxt-link to="/" no-prefetch exact active-class-exact="active" class="main-logo">NUXT SSR</nuxt-link>
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
      <b-collapse id="nav-collapse" class="my-collapse" is-nav>
        <b-navbar-nav class="nav-links">
          <nuxt-link  no-prefetch active-class="active" to="/films" class="nav-link">Films</nuxt-link>
          <nuxt-link  no-prefetch active-class="active" to="/users" class="nav-link">Heroes</nuxt-link>
          <nuxt-link  no-prefetch active-class="active" to="/planets" class="nav-link">Planets</nuxt-link>
          <nuxt-link  no-prefetch active-class="active" to="/starships" class="nav-link">Star Ships</nuxt-link>
          <nuxt-link  no-prefetch active-class="active" to="/species" class="nav-link">Species</nuxt-link>
          <nuxt-link  no-prefetch active-class="active" to="/about" class="nav-link">About Me</nuxt-link>
          <nuxt-link  no-prefetch active-class="active" to="/work" class="nav-link">Work</nuxt-link>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template #button-content>
              <em>User</em>
            </template>
            <nuxt-link  no-prefetch active-class="active" to="/login" class="dropdown-item">Войти</nuxt-link>
            <nuxt-link  no-prefetch active-class="active" to="/logout" class="dropdown-item">Выйти</nuxt-link>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
    export default {
        name: "Navbar"
    }
</script>

<style scoped lang="scss">
  .dropdown-menu{
    min-width: 3rem !important;
  }
  .main-logo{
    -webkit-transition: background-color 1000ms linear;
    -ms-transition: background-color 1000ms linear;
    transition: background-color 1000ms linear;
    font-size: 36px;
    color: #5c4a4aa6;
    text-decoration: none;
    margin-right: 15px;
  }
  .nav-link{
    font-size: 20px;
    color: #421d1d;
    text-decoration: none;
  }
  .my-navbar{
    padding: 15px 30px;
  }
  .my-collapse{
    justify-content: space-between;
  }
  .nuxt-link-active{
    background: -webkit-linear-gradient(315deg,#42d392 25%,#647eff);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .nav-links{
    a{
      color: #421d1d;
      -webkit-transition: background-color 1000ms linear;
      -ms-transition: background-color 1000ms linear;
      transition: background-color 1000ms linear;
    }
  }

</style>
