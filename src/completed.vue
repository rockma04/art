<script setup>
  import { onMounted, ref} from "vue"
  import PageHeader from "./components/pageHeader.vue"

  const galleries = ref([])
  const loading = ref(true)
  const error = ref('')

  async function loadGalleries() {
    loading.value = true
    error.value = ''

    try {
      const response = await fetch('/api/galleries')

      if (!response.ok) {
        throw new Error ('Failed to load galleries')
      }
      const data = await response.json();

      galleries.value = data.map((gallery) => ({
        id: gallery.id,
        style: gallery.style,
        description: gallery.description,
        link: gallery.link
      }))
    } catch (err) {
      error.value = err.message || 'Error trying to load galleries'
    } finally {
      loading.value = false
    }
  }

  onMounted(() => {
    loadGalleries()
  })
</script>

<template>
  <PageHeader title="Completed Projects" description="Check out the galleries below which include the different projects that have been completed."></PageHeader>

  <v-container>
    <v-row>
      <v-col
          cols="4"
          class="flex"
          v-for="gallery in galleries"
       >
        <v-card
          color="red-accent-1"
          class="pa-2"
        >
          <v-card-title
          class="text-center text-white"
          >{{ gallery.style }}</v-card-title>
          <v-container>
            <v-row class="align-center justify-center flat">
              <v-btn
                  class="align-center justify-center v-btn--flat"
                  height="25"
                  color="red"
                  :href="gallery.link"
              >View Gallery
              </v-btn>
            </v-row>
          </v-container>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>

</style>