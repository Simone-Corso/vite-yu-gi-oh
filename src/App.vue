<template>
  <div>
    <header>
      
      <select v-model="selectedArchetype" @change="filterByArchetype">
        <option value="">Tutti gli Archetipi</option>
        <option v-for="archetype in archetypes" :key="archetype" :value="archetype">{{ archetype }}</option>
      </select>
    </header>

    <div class="container">
      <div class="card-container">
        <Card v-for="card in filteredCards" :key="card.id" :data="card" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Card from './components/AppCard.vue';

export default {
  components: {
    Card,
  },
  data() {
    return {
      cards: [],
      archetypes: [],
      selectedArchetype: '',
    };
  },
  computed: {
    filteredCards() {
      return this.selectedArchetype
        ? this.cards.filter((card) => card.archetype === this.selectedArchetype)
        : this.cards;
    },
  },
  created() {
    this.fetchCards();
    this.fetchArchetypes();
  },
  methods: {
    async fetchCards() {
      try {
        const response = await axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0');
        this.cards = response.data.data;
      } catch (error) {
        console.error('Error fetching cards:', error);
      }
    },
    async fetchArchetypes() {
      try {
        const response = await axios.get('https://db.ygoprodeck.com/api/v7/archetypes.php');
        this.archetypes = response.data;
      } catch (error) {
        console.error('Error fetching archetypes:', error);
      }
    },
    filterByArchetype() {
      
      const url = this.selectedArchetype
        ? `https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0&archetype=${this.selectedArchetype}`
        : 'https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0';

      this.fetchCardsWithArchetype(url);
    },
    async fetchCardsWithArchetype(url) {
  try {
    const response = await axios.get(url);
    this.cards = response.data.data;
  } catch (error) {
    console.error('Error fetching cards with archetype:', error);
  }
},
  },
};
</script>

<style>
.card-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.container{
  width: 1000px;
  height: auto;
  display: flex;
justify-content: center;
}

body{
  display: flex;
  justify-content: center;
}
</style>


