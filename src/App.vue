<template>
  <v-app class="custom-background">
    <v-container>
      <h1 class="text-h4 mb-4 text-white">Galería de Imágenes</h1>
      
      <v-tabs v-model="currentTab" color="deep-purple-accent-2">
        <v-tab value="gallery">Galería Completa</v-tab>
        <v-tab value="favorites">Favoritos</v-tab>
      </v-tabs>

      <Gallery
        v-if="currentTab === 'gallery'"
        :favorites="favorites"
        @open-modal="openImage"
        @toggle-favorite="toggleFavorite"
      />

      <Favorites
        v-if="currentTab === 'favorites'"
        :favorites="favorites"
        @open-modal="openImage"
        @toggle-favorite="toggleFavorite"
      />

      <ImageModal
        :image="selectedImage"
        :show="showModal"
        @close="showModal = false"
      />
    </v-container>
  </v-app>
</template>

<script>
import Gallery from './components/Gallery.vue';
import Favorites from './components/Favorites.vue';
import ImageModal from './components/ImageModal.vue';

export default {
  components: { Gallery, Favorites, ImageModal },
  data: () => ({
    currentTab: 'gallery',
    showModal: false,
    selectedImage: null,
    favorites: [],
  }),
  methods: {
    openImage(img) {
      this.selectedImage = img;
      this.showModal = true;
    },
    toggleFavorite(img) {
      const index = this.favorites.findIndex(f => f.id === img.id);
      if (index >= 0) this.favorites.splice(index, 1);
      else this.favorites.push(img);
    },
  },
};
</script>

<style>
.custom-background {
  background-color: #1e1e2f !important;
  min-height: 100vh;
}
</style>
