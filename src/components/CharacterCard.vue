<template>
  <div class="character-card">
    <div class="content-wrapper">
      <div class="image-container">
        <img v-if="character.image" :src="character.image" alt="Character image">
        <div v-else class="placeholder"></div>
      </div>
      <div class="text-container">
        <p>{{ character.name }}</p>
        <p>{{ character.status }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    character: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style>
.character-card {
  display: flex;
  border-radius: 10px;
  background-color: white;
  margin: 10px;
  position: relative;
}

.content-wrapper {
  display: flex;
  width: 100%;
}

.image-container {
  flex: 1;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;

  img {
    width: 100%;
    height: 100%;
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px;
  }
}

.text-container {
  flex: 1;
  padding: 10px;

  p {
    font-family: -apple-system, 'BlinkMacSystemFont', 'Segoe UI', 'Roboto', 'Helvetica', 'Arial', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';
    font-weight: 800;
  }
}

.placeholder {
  width: 100%;
  height: 100%;
  background-color: #f0f0f0;
}
</style>