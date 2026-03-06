<script setup>
import GalleryGrid from "./components/galleryGrid.vue"
import PageHeader from "@/components/pageHeader.vue";

const final = [
  {
    description: 'Test',
    image: 'photo_1.jpg'
  },
  {
    description: 'Test',
    image: 'photo_2.jpg'
  },
  {
    description: 'Test',
    image: 'photo_4.jpg'
  },
  {
    description: 'Test',
    image: 'photo_3.jpg'
  },
  {
    description: 'Test',
    image: 'photo_5.jpg'
  },
  {
    description: 'Test',
    image: 'photo_6.jpg'
  },
  {
    description: 'Test',
    image: 'photo_7.jpg'
  },
  {
    description: 'Test',
    image: 'photo_8.jpg'
  },
  {
    description: 'Test',
    image: 'photo_10.jpg'
  },
  {
    description: 'Test',
    image: 'photo_11.jpg'
  },
  {
    description: 'Test',
    image: 'photo_12.jpg'
  },
  {
    description: 'Test',
    image: 'photo_13.jpg'
  },
  {
    description: 'Test',
    image: 'photo_14.jpg'
  },
  {
    description: 'Test',
    image: 'photo_15.jpg'
  },
  {
    description: 'Test',
    image: 'photo_16.jpg'
  },
  {
    description: 'Test',
    image: 'photo_17.jpg'
  },
  {
    description: 'Test',
    image: 'photo_18.jpg'
  },
  {
    description: 'Test',
    image: 'photo_19.jpg'
  },
  {
    description: 'Test',
    image: 'photo_20.jpg'
  },
  {
    description: 'Test',
    image: 'photo_21.jpg'
  },
  {
    description: 'Test',
    image: 'photo_22.jpg'
  },
  {
    description: 'Test',
    image: 'photo_23.jpg'
  },
  {
    description: 'Test',
    image: 'photo_24.jpg'
  },
  {
    description: 'Test',
    image: 'photo_25.jpg'
  },
]
</script>

<template>
  <PageHeader title="Photo Gallery" description="Nature, Landscapes, Portraits, Still Lives"></PageHeader>

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
