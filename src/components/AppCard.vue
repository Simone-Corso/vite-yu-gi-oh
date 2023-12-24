<template>
    <div class="card">
      <img :src="data.card_images[0].image_url" alt="Card Image" />
      <h3>{{ data.name }}</h3>
      <h2>Alien</h2>
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
    margin: 10px;
    width: 150px; 
    background-color: #D48F38;
  }
  
  .card img {
    max-width: 100%;
    height: auto;
  }

h2{
    text-align: center;
  }

  h3{
    text-align: center;
    color: white;
  }
  
  </style>
  
