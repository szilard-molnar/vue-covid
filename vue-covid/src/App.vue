<template>
  <div id="app">
    <div class="title">
          <h1>Covid tracker Vue.js</h1>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
    
  }
}
</script>

<style lang="scss" scoped> 
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
    background-color: rgba(105, 230, 252, 0.194);
  }
</style>
