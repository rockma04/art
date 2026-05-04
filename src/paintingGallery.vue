<script setup>
import { onMounted, ref } from "vue"
import GalleryGrid from "./components/galleryGrid.vue"
import PageHeader from "@/components/pageHeader.vue";

const paintings = ref([])
const loading = ref(true)
const error = ref('')

async function loadPaintings() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('/api/paintings')

    if (!response.ok) {
      throw new Error('Failed to load paintings')
    }
    const data = await response.json();

    paintings.value = data.map((paint) => ({
      id: paint.id,
      description: paint.description,
      image: paint.image,
      completed: paint.completed
    }))
  } catch (err) {
    error.value = err.message || 'Error while trying to load paintings'
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  loadPaintings()
})
</script>

<template>
  <PageHeader title="Paintings" description="Acrylic, Oil, Watercolor"></PageHeader>

  <v-container
      class="hidden-sm-and-down"
      fluid
  >
    <v-row>
      <v-col
          v-for="paint in paintings"
          :key="paint.description"
          cols="4"
          class="flex"
      >
        <GalleryGrid
            :image="paint.image"
            :description="paint.description"
            :completed="paint.completed"
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
          v-for="paint in paintings"
          :key="paint.description"
          cols="6"
      >
        <GalleryGrid
            :image="paint.image"
            :description="paint.description"
            :completed="paint.completed"
        >
        </GalleryGrid>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>

</style>