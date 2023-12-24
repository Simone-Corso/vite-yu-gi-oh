<template>
  <div class="card-container">
    <Card v-for="card in cards" :key="card.id" :data="card" />
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
    };
  },
  created() {
    this.fetchCards();
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
  },
};
</script>

<style>
.card-container {
}
</style>

