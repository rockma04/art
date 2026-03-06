<script setup>
import GalleryGrid from "./components/galleryGrid.vue"
import PageHeader from "@/components/pageHeader.vue";

const final = [
  {
    description: 'Night View',
    image: 'cp_1.jpg'
  },
  {
    description: 'Football Player',
    image: 'painting_1.JPG'
  },
  {
    description: 'Spring Farming',
    image: 'painting_2.jpg'
  },
  {
    description: 'Golden Night',
    image: 'dress_1.jpg'
  },
  {
    description: 'Patriotic Dress',
    image: 'dress_2.jpg'
  },
  {
    description: 'Feeling Blue',
    image: 'dress_3.jpg'
  },
]
</script>

<template>
  <PageHeader title="Additional Pieces Gallery" description="Collage, Colored Pencil, Painting"></PageHeader>

  <v-container>
    <v-row>
      <v-col
          v-for="fin in final"
          :key="fin.description"
          cols="4"
          class="flex"
      >
        <GalleryGrid
            :image="fin.image"
            :description="fin.description">
        </GalleryGrid>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>

</style>