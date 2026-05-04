<script setup>
import { onMounted, ref } from "vue"
import GalleryGrid from "./components/galleryGrid.vue"
import PageHeader from "@/components/pageHeader.vue";

const otherProjects = ref([])
const loading = ref(true)
const error = ref('')

async function loadOtherProjects() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('/api/otherProjects')

    if (!response.ok) {
      throw new Error('Failed to load other projects')
    }
    const data = await response.json();

    otherProjects.value = data.map((other) => ({
      id: other.id,
      description: other.description,
      image: other.image,
      completed: other.completed
    }))
  } catch (err) {
    error.value = err.message || 'Error while trying to load other projects'
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  loadOtherProjects()
})
</script>

<template>
  <PageHeader title="Other Projects" description="Door Signs, Flower Pots, Glasses, Guitars"></PageHeader>

  <v-container
      class="hidden-sm-and-down"
      fluid
  >
    <v-row>
      <v-col
          v-for="other in otherProjects"
          :key="other.description"
          cols="4"
          class="flex"
      >
        <GalleryGrid
            :image="other.image"
            :description="other.description"
            :completed="other.completed"
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
          v-for="other in otherProjects"
          :key="other.description"
          cols="6"
      >
        <GalleryGrid
            :image="other.image"
            :description="other.description"
            :completed="other.completed"
        >
        </GalleryGrid>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>

</style>