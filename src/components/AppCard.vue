<template>
    <div class="card">
      <h3>{{ data.name }}</h3>
      <img :src="data.card_images[0].image_url" alt="Card Image" />
      <p>{{ data.desc }}</p>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      data: {
        type: Object,
        required: true,
      },
    },
  };
  </script>
  
  <style scoped>
  .card {
    border: 1px solid #ccc;


  }
  </style>
  

