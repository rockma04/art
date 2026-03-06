<script setup>
import GalleryGrid from "./components/galleryGrid.vue"
import PageHeader from "@/components/pageHeader.vue";

const final = [
  {
    description: 'Test',
    image: 'print_1.jpg'
  },
  {
    description: 'Test',
    image: 'print_2.jpg'
  },
  {
    description: 'Test',
    image: 'print_3.jpg'
  },
  {
    description: 'Test',
    image: 'print_4.jpg'
  },
  {
    description: 'Test',
    image: 'print_5.jpg'
  },
  {
    description: 'Test',
    image: 'print_18.jpg'
  },
  {
    description: 'Test',
    image: 'print_7.jpg'
  },
  {
    description: 'Test',
    image: 'print_8.jpg'
  },
  {
    description: 'Test',
    image: 'print_9.jpg'
  },
  {
    description: 'Test',
    image: 'print_10.jpg'
  },
  {
    description: 'Test',
    image: 'print_11.jpg'
  },
  {
    description: 'Test',
    image: 'print_12.jpg'
  },
  {
    description: 'Test',
    image: 'print_13.jpg'
  },
  {
    description: 'Test',
    image: 'print_14.jpg'
  },
  {
    description: 'Test',
    image: 'print_15.jpg'
  },
  {
    description: 'Test',
    image: 'print_16.jpg'
  },
  {
    description: 'Test',
    image: 'print_17.jpg'
  },
  {
    description: 'Test',
    image: 'print_18.jpg'
  },
  {
    description: 'Test',
    image: 'print_19.jpg'
  },
  {
    description: 'Test',
    image: 'print_20.jpg'
  },
]
</script>

<template>
  <PageHeader title="Prints" description="Etching, Monoprints, Photo Transfer, Relief Prints"></PageHeader>

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