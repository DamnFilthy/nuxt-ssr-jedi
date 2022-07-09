<template>
  <div>
    <nuxt-link  no-prefetch active-class="active" to="/">На главную</nuxt-link>
    <div class="empty-layout">
      <nuxt/>
    </div>
  </div>
</template>

<style scoped lang="scss">
.empty-layout{
  display: flex;
  justify-content: center;
  padding: 5rem 1rem;
}
</style>
