<template>
  <div>
    <Navbar/>
    <main>
      <div class="container">
        <Nuxt />
      </div>
    </main>
  </div>
</template>

<style lang="scss">
  @font-face {
    font-family: 'StarJedi';
    src: url(assets/fonts/starjedi/SoloistLaser.eot?) format('eot'),
    url(assets/fonts/starjedi/SoloistLaser.woff) format('woff'),
    url(assets/fonts/starjedi/SoloistLaser.ttf) format('truetype');
    font-weight: 700;
  }
  body{
    background-color: #1c1e22;
    color: #c8c8c8;
  }
  h1, a{
    font-family: 'StarJedi', sans-serif;
  }
  h1{
    text-align: center;
    color: #ffe300;
    margin: 50px 0;
  }
  section{
    margin-top: 50px;
  }

  .list-block{
   display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
  .list-item{
    background-color: #272b30;
    box-shadow: 5px 5px 10pxrgba(0,0,0,.25);
    cursor: pointer;
    min-width: 300px;
    height: 200px;
    text-align: start;
    transition: transform .3s;
    list-style-type: none;
    margin-right: 30px;
    margin-top: 15px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-decoration: none;
    color: #fff;
    &:hover {
      box-shadow: 0 5px 20px #ffe300;
      transform: translateY(-8px);
      color: #ffe300;
    }
  }
  .jedi{
    font-family: 'StarJedi', sans-serif;
  }

</style>
