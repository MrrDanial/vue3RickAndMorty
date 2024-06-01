<template>
  <div>
    <div class="filter-container">
      <input type="text" v-model="nameFilter" placeholder="Фильтр по имени" class="filter-input">
      <select v-model="statusFilter" class="filter-select">
        <option value="">Все статусы</option>
        <option value="Alive">Живой</option>
        <option value="Dead">Мертвый</option>
        <option value="unknown">Неизвестно</option>
      </select>
      <button @click="applyFilters" class="filter-button">Применить</button>
    </div>

    <div class="characters-container">
      <div class="character-card" v-for="character in characters" :key="character.id">
        <CharacterCard :character="character" />
      </div>
    </div>
    <footer>
      <div>
        <button @click="prevPage" :disabled="page === 1">Предыдущая страница</button>
        <span>Страница {{ page }} / {{ totalPages }}</span>
        <button @click="nextPage" :disabled="page === totalPages">Следующая страница</button>
      </div>
      <p>©Rick and Morty, Daniil Serdiukov</p>
    </footer>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import CharacterCard from './CharacterCard.vue';

export default {
  components: {
    CharacterCard,
  },
  setup() {
    const characters = ref([]);
    const page = ref(1);
    const totalPages = ref(1);
    const nameFilter = ref('');
    const statusFilter = ref('');
    const currentPage = ref(1);

    const fetchCharacters = async () => {
      const response = await fetch(`https://rickandmortyapi.com/api/character?page=${page.value}&name=${nameFilter.value}&status=${statusFilter.value}`);
      const data = await response.json();
      characters.value = data.results;
      totalPages.value = data.info.pages;
    };

    const nextPage = () => {
      if (page.value < totalPages.value) {
        page.value++;
        fetchCharacters();
      }
    };

    const prevPage = () => {
      if (page.value > 1) {
        page.value--;
        fetchCharacters();
      }
    };

    const applyFilters = () => {
      page.value = 1;
      fetchCharacters();
    };

    onMounted(() => {
      fetchCharacters();
    });

    return {
      characters,
      page,
      totalPages,
      nameFilter,
      statusFilter,
      nextPage,
      prevPage,
      applyFilters,
      currentPage,
    };
  },
};
</script>

<style>
.characters-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  align-items: normal;
}

.filter-container {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
}

.filter-input,
.filter-select {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
}

.filter-button {
  padding: 8px 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;

  &:hover {
    background-color: #45a049;
  }

  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
    background-color: #ccc;
  }
}
</style>