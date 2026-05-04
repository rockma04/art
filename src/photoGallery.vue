<script setup>
import { onMounted, ref } from "vue"
import GalleryGrid from "./components/galleryGrid.vue"
import PageHeader from "@/components/pageHeader.vue";

const photos = ref([])
const loading = ref(true)
const error = ref('')

async function loadPhotos() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('/api/photography')

    if (!response.ok) {
      throw new Error('Failed to load photos')
    }
    const data = await response.json();

    photos.value = data.map((photo) => ({
      id: photo.id,
      description: photo.description,
      image: photo.image,
      completed: photo.completed
    }))
  } catch (err) {
    error.value = err.message || 'Error while trying to load photos'
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  loadPhotos()
})
</script>

<template>
  <PageHeader title="Photo Gallery" description="Nature, Landscapes, Portraits, Still Lives"></PageHeader>

  <v-container
  class="hidden-sm-and-down"
  fluid
  >
    <v-row>
      <v-col
          v-for="photo in photos"
          :key="photo.description"
          cols="4"
          class="flex"
      >
        <GalleryGrid
            :image="photo.image"
            :description="photo.description"
            :completed="photo.completed"
        >
        </GalleryGrid>
      </v-col>
    </v-row>
  </v-container>

  <v-container
      class="d-xs-flex d-md-none"
      fluid
  >
    <v-row>
      <v-col
          v-for="photo in photos"
          :key="photo.description"
          cols="6"
      >
        <GalleryGrid
            :image="photo.image"
            :description="photo.description"
            :completed="photo.completed"
        >
        </GalleryGrid>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>

</style>
