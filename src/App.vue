<template>
  <div class="container">
    <header>
      <h1>Rick and Morty Character List</h1>
    </header>
    <div>
      <CharacterList />
    </div>
  </div>
</template>

<script>
import CharacterList from './components/CharacterList.vue';
export default {
  components: {
    CharacterList,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  margin: 0;
  padding: 0;
  overflow: auto;
}

.container {
  background-image: url('@/assets/Rick-And-Morty-4k.jpeg');
  background-size: cover;
  background-position: center;
  height: 100%;
}

header,
footer {
  background-color: #333;
  color: white;
  padding: 10px;
  text-align: center;
}
</style>