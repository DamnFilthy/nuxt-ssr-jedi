<template>
  <button @click="$emit('showMore')">
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    Show more
  </button>
</template>

<script>
  export default {
    name: "show-more-btn"
  }
</script>

<style lang="scss" scoped>
  button {
    display: flex;
    margin: 40px auto 40px auto;
    background-color: #1c1e22;
    border: none;
    outline: none;
    position: relative;
    padding: 10px 20px;
    color: #ffe300;
    font-size: 16px;
    text-decoration: none;
    text-transform: uppercase;
    overflow: hidden;
    transition: .5s;
    letter-spacing: 4px
  }

  button:hover {
    background: #ffe300;
    color: #1c1e22;
    border-radius: 2px;
    box-shadow: 0 0 2px #ffe300,
    0 0 25px #ffe300,
    0 0 50px #ffe300,
    0 0 100px #ffe300;
  }

  button span {
    position: absolute;
    display: block;
  }

  button span:nth-child(1) {
    top: 0;
    left: -100%;
    width: 100%;
    height: 2px;
    background: linear-gradient(90deg, transparent, #ffe300);
    animation: btn-anim1 1s linear infinite;
  }

  button span:nth-child(2) {
    top: -100%;
    right: 0;
    width: 2px;
    height: 100%;
    background: linear-gradient(180deg, transparent, #ffe300);
    animation: btn-anim2 1s linear infinite;
    animation-delay: .25s
  }

  button span:nth-child(3) {
    bottom: 0;
    right: -100%;
    width: 100%;
    height: 2px;
    background: linear-gradient(270deg, transparent, #ffe300);
    animation: btn-anim3 1s linear infinite;
    animation-delay: .5s
  }

  button span:nth-child(4) {
    bottom: -100%;
    left: 0;
    width: 2px;
    height: 100%;
    background: linear-gradient(360deg, transparent, #ffe300);
    animation: btn-anim4 1s linear infinite;
    animation-delay: .75s
  }

  @keyframes btn-anim1 {
    0% {
      left: -100%;
    }
    50%, 100% {
      left: 100%;
    }
  }

  @keyframes btn-anim2 {
    0% {
      top: -100%;
    }
    50%, 100% {
      top: 100%;
    }
  }

  @keyframes btn-anim3 {
    0% {
      right: -100%;
    }
    50%, 100% {
      right: 100%;
    }
  }

  @keyframes btn-anim4 {
    0% {
      bottom: -100%;
    }
    50%, 100% {
      bottom: 100%;
    }
  }
</style>
