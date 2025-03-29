<template>
    <div>
      <v-row justify="center" v-if="loading" class="my-12">
        <v-progress-circular indeterminate color="deep-purple-accent-2" size="70" width="7"/>
      </v-row>
  
      <v-row v-else>
        <v-col v-for="img in images" :key="img.id" cols="12" sm="6" md="4">
          <v-card class="custom-card" @click="$emit('open-modal', img)">
            <v-img :src="img.download_url" :alt="img.author" height="200px">
              <v-btn icon color="red-lighten-1" class="favorite-btn" @click.stop="$emit('toggle-favorite', img)">
                <v-icon>{{ favorites.some(fav => fav.id === img.id) ? 'mdi-heart' : 'mdi-heart-outline' }}</v-icon>
              </v-btn>
            </v-img>
            <v-card-title>{{ img.author }}</v-card-title>
          </v-card>
        </v-col>
      </v-row>
  
      <v-row justify="center" class="mt-6">
        <v-pagination v-model="currentPage" :length="totalPages" @update:model-value="fetchImages" color="deep-purple-accent-2"/>
      </v-row>
    </div>
  </template>
  
  <script>
  export default {
    props: ['favorites'],
    data() {
      return {
        images: [],
        loading: false,
        currentPage: 1,
        totalPages: 10,
      };
    },
    mounted() {
      this.fetchImages();
    },
    methods: {
      fetchImages() {
        this.loading = true;
        fetch(`https://picsum.photos/v2/list?page=${this.currentPage}&limit=12`)
          .then(res => res.json())
          .then(data => this.images = data)
          .catch(console.error)
          .finally(() => this.loading = false);
      },
    },
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
  