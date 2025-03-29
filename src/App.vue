<template>
  <v-app class="custom-background">
    <v-container>
      <v-row>
        <v-col cols="12">
          <h1 class="text-h4 mb-4 text-white">Galería de Imágenes</h1>
        </v-col>
      </v-row>

      <!-- Loader -->
      <v-row justify="center" v-if="loading" class="my-12">
        <v-progress-circular
          indeterminate
          color="deep-purple-accent-2"
          size="70"
          width="7"
        />
      </v-row>

      <!-- Imágenes -->
      <v-row v-else>
        <v-col
          v-for="img in images"
          :key="img.id"
          cols="12"
          sm="6"
          md="4"
        >
          <v-card class="custom-card" @click="openImage(img)">
            <v-img :src="img.download_url" :alt="img.author" height="200px" />
            <v-card-title>{{ img.author }}</v-card-title>
          </v-card>
        </v-col>
      </v-row>

      <!-- Paginación -->
      <v-row justify="center" class="mt-6">
        <v-pagination
          v-model="currentPage"
          :length="totalPages"
          @update:model-value="fetchImages"
          color="deep-purple-accent-2"
        />
      </v-row>

      <!-- Modal -->
      <v-dialog v-model="showModal" max-width="800">
        <v-card>
          <v-img :src="selectedImage?.download_url" height="500px" cover />
          <v-card-title>{{ selectedImage?.author }}</v-card-title>
          <v-card-actions>
            <v-spacer />
            <v-btn color="red-darken-1" @click="showModal = false">Cerrar</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-container>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      images: [],
      showModal: false,
      selectedImage: null,
      currentPage: 1,
      totalPages: 10,
      loading: false,
    };
  },
  mounted() {
    this.fetchImages(this.currentPage);
  },
  methods: {
    openImage(img) {
      this.selectedImage = img;
      this.showModal = true;
    },
    fetchImages(page) {
      this.loading = true;
      fetch(`https://picsum.photos/v2/list?page=${page}&limit=12`)
        .then(res => res.json())
        .then(data => {
          this.images = data;
        })
        .catch(err => console.error(err))
        .finally(() => {
          this.loading = false;
        });
    },
  },
};
</script>

<style>
.custom-background {
  background-color: #1e1e2f;
  min-height: 100vh;
}

.custom-card {
  background-color: #2a2a3c;
  color: white;
  cursor: pointer;
  transition: transform 0.2s ease;
}
.custom-card:hover {
  transform: scale(1.02);
}
</style>
