<script setup>
import { onMounted, ref } from "vue"
import GalleryGrid from "./components/galleryGrid.vue"
import PageHeader from "@/components/pageHeader.vue";

const collages = ref([])
const loading = ref(true)
const error = ref('')

async function loadCollages() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('/api/collage')

    if (!response.ok) {
      throw new Error('Failed to load collages')
    }
    const data = await response.json();

    collages.value = data.map((collage) => ({
      id: collage.id,
      description: collage.description,
      image: collage.image,
      completed: collage.completed
    }))
  } catch (err) {
    error.value = err.message || 'Error while trying to load collages'
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  loadCollages()
})
</script>

<template>
  <PageHeader title="Collages" description="Paper, Paint, Ink"></PageHeader>

  <v-container
      class="hidden-sm-and-down"
      fluid
  >
    <v-row>
      <v-col
          v-for="collage in collages"
          :key="collage.description"
          cols="4"
          class="flex"
      >
        <GalleryGrid
            :image="collage.image"
            :description="collage.description"
            :completed="collage.completed"
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
          v-for="collage in collages"
          :key="collage.description"
          cols="6"
      >
        <GalleryGrid
            :image="collage.image"
            :description="collage.description"
            :completed="collage.completed"
        >
        </GalleryGrid>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>

</style>