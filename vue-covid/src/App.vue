<template>
  <div id="app">
    <div class="title">
          <h1>Covid Tracker Vue.js</h1>
    </div>
    <div class="cards animate__animated ">
      <Confirmed />
      <Recovered />
      <Dead />
    </div>
  </div>
</template>

<script>
import Confirmed from './components/Confirmed';
import Dead from './components/Dead';
import Recovered from './components/Recovered';

export default {
  name: 'App',
  components: {
    Confirmed,
    Dead,
    Recovered,
  },

  mounted() {
    document.querySelector(".cards").classList.add("animate__zoomIn");
  }
}
</script>

<style lang="scss"> 
  #app {
    height: 100vh;
    background-color: rgb(255, 255, 180);
  }

  .title {
    height: 100px;
    border-bottom: 2px solid rgba(0, 60, 255, 0.612);
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .cards {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    column-gap: 20px;
    width: 90%;
    margin: auto;
    margin-top: 50px;
  }
</style>
