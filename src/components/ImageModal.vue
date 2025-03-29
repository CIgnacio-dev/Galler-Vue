<template>
    <v-dialog :model-value="show" @update:model-value="$emit('close')" max-width="800">
      <v-card>
        <v-img :src="image?.download_url" height="500px" cover />
        <v-card-title>{{ image?.author }}</v-card-title>
        <v-card-actions>
          <v-spacer />
          <v-btn color="red-darken-1" @click="$emit('close')">Cerrar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </template>
  
  <script>
  export default {
    props: {
      image: Object,
      show: Boolean,
    },
  };
  </script>
  