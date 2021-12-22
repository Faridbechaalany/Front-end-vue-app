<template>
  <div id="app">
    <header>
      <div class="title">{{title}}</div>
    </header>

    <section class="main-content w-50 mx-auto">
      <h1>Menu</h1>
      <p>expand to see the rooms and windows...</p>
      <buildings-list></buildings-list>
    </section>
  </div>
</template>

<script>
import BuildingsList from './components/BuildingsList';

export default {
  name: 'App',
  components: {
    BuildingsList
},
  data: function() {
      return {
      title: 'Welcome to our website where you can manage your buildings, rooms and windows'
    }
  }
}
</script>

<style lang="scss" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #041422;
  margin-top: 60px;
}

.title{
  font-size: xx-large;
}

h1 {
  color:rgb(23, 2, 212);
  margin-top: 60px;
}

p {
  margin-top: 30px;
}

</style>
