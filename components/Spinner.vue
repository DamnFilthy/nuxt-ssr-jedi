<template>
  <div class="spinner__wrapper">
    <div id="spinner"></div>
  </div>
</template>

<script>
  export default {
    name: "Spinner"
  }
</script>

<style scoped>
  #spinner {
    display: inline-block;
    width: 50px;
    height: 50px;
    border: 4px solid rgba(255, 255, 255, .3);
    border-radius: 50%;
    border-top-color: #ffe300;
    animation: spin 1s ease-in-out infinite;
    -webkit-animation: spin 1s ease-in-out infinite;
  }

  .spinner__wrapper {
    padding: 40px 0;
    display: flex;
    justify-content: center;
  }

  @keyframes spin {
    to {
      -webkit-transform: rotate(360deg);
    }
  }

  @-webkit-keyframes spin {
    to {
      -webkit-transform: rotate(360deg);
    }
  }
</style>
