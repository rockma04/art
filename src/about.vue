<script setup>
  import {ref} from "vue"
  import ProjectCarousel from "./components/projectCarousel.vue"

  const projects = [
    {
      style: 'Colored Pencil',
      description: 'Landscapes, Portraits, Nature, and Still Lives.',
      image: 'completed.jpg'
    },
    {
      style: 'Painting',
      description: 'Landscapes, Portraits, Nature, and Still Lives.',
      image: 'completed.jpg'
    },
    {
      style: 'Photography',
      description: 'Landscapes, Portraits, Nature, and Still Lives.',
      image: 'completed.jpg'
    },
    {
      style: 'Prints',
      description: 'Landscapes, Portraits, Nature, and Still Lives.',
      image: 'completed.jpg'
    },
    {
      style: 'Other',
      description: 'Landscapes, Portraits, Nature, and Still Lives.',
      image: 'completed.jpg'
    },
  ]
</script>

<template>
  <h1>SWITCH TO TABS INSTEAD OF CARDS</h1>
  <v-row>
    <v-col
      v-for="pro in projects"
      cols="12"
      sm="6"
      md="4">
      <ProjectCarousel
          :style="pro.style"
          :description="pro.description"
          :image="pro.image"></ProjectCarousel>
    </v-col>
  </v-row>
</template>

<style scoped>

</style>