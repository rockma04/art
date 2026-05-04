<script setup>
import { onMounted, ref } from "vue"
import GalleryGrid from "./components/galleryGrid.vue"
import PageHeader from "@/components/pageHeader.vue";

const prints = ref([])
const loading = ref(true)
const error = ref('')

async function loadPrints() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('/api/prints')

    if (!response.ok) {
      throw new Error('Failed to load prints')
    }
    const data = await response.json();

    prints.value = data.map((print) => ({
      id: print.id,
      description: print.description,
      image: print.image,
      completed: print.completed
    }))
  } catch (err) {
    error.value = err.message || 'Error while trying to load prints'
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  loadPrints()
})
</script>

<template>
  <PageHeader title="Prints" description="Etching, Monoprints, Photo Transfer, Relief Prints"></PageHeader>

  <v-container
      class="hidden-sm-and-down"
      fluid
  >
    <v-row>
      <v-col
          v-for="print in prints"
          :key="print.description"
          cols="4"
          class="flex"
      >
        <GalleryGrid
            :image="print.image"
            :description="print.description"
            :completed="print.completed"
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
          v-for="print in prints"
          :key="print.description"
          cols="6"
      >
        <GalleryGrid
            :image="print.image"
            :description="print.description"
            :completed="print.completed"
        >
        </GalleryGrid>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>

</style>