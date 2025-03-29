<template>
    <div>
      <v-row v-if="favorites.length > 0">
        <v-col v-for="img in favorites" :key="img.id" cols="12" sm="6" md="4">
          <v-card class="custom-card" @click="$emit('open-modal', img)">
            <v-img :src="img.download_url" :alt="img.author" height="200px">
              <v-btn icon color="red-lighten-1" class="favorite-btn" @click.stop="$emit('toggle-favorite', img)">
                <v-icon>mdi-heart</v-icon>
              </v-btn>
            </v-img>
            <v-card-title>{{ img.author }}</v-card-title>
          </v-card>
        </v-col>
      </v-row>
  
      <v-row v-else justify="center" class="my-10">
        <span class="text-h6 text-grey">Aún no tienes favoritos ❤️</span>
      </v-row>
    </div>
  </template>
  
  <script>
  export default {
    props: ['favorites'],
  };
  </script>
  
  <style scoped>
  .custom-card {
    background-color: #2a2a3c !important;
    color: white !important;
    cursor: pointer;
    transition: transform 0.2s ease;
    border: 1px solid #3e3e55 !important;
  }
  
  .custom-card:hover {
    transform: scale(1.02);
    border-color: #676785 !important;
  }
  
  .favorite-btn {
    position: absolute !important;
    top: 8px;
    right: 8px;
    z-index: 1;
  }
  </style>
  