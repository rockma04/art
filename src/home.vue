<script setup>
  import { onMounted, ref } from 'vue'

  const tab = ref(null)

  const pages = ref([])
  const tabs = ref([])
  const carousels = ref([])
  const loading = ref(true)
  const error = ref('')

  async function loadPages() {
    loading.value = true
    error.value = ''

    try{
      const response = await fetch('/api/pages')

      if (!response.ok) {
        throw new Error('Failed to load pages')
      }
      const data = await response.json();

      pages.value = data.map((page) => ({
        id: page.id,
        title: page.title,
        subtitle: page.subtitle,
        image: page.image,
        link: page.link,
        flex: page.flex
      }))
    } catch (err) {
      error.value = err.message || 'Error while trying to load pages'
    } finally {
      loading.value = false
    }
  }

  async function loadTabs() {
    loading.value = true
    error.value = ''

    try{
      const response = await fetch('/api/tabs')

      if (!response.ok) {
        throw new Error('Failed to load tabs')
      }
      const data = await response.json();

      tabs.value = data.map((tab) => ({
        id: tab.id,
        title: tab.title,
        image: tab.image,
        text: tab.text
      }))
    } catch (err) {
      error.value = err.message || 'Error while trying to load tabs'
    } finally {
      loading.value = false
    }
  }

  async function loadCarousel() {
    loading.value = true
    error.value = ''

    try{
      const response = await fetch('/api/homeCarousel')

      if (!response.ok) {
        throw new Error('Failed to load carousel')
      }
      const data = await response.json();

      carousels.value = data.map((carousel) => ({
        id: carousel.id,
        image: carousel.image
      }))
    } catch (err) {
      error.value = err.message || 'Error while trying to load carousel'
    } finally {
      loading.value = false
    }
  }

  onMounted(() => {
    loadPages()
    loadTabs()
    loadCarousel()
  })

</script>

<template>
  <v-carousel
      class="hidden-sm-and-down"
      height="675"
      cycle
      delimiter-icon="mdi-palette-outline"
  >

    <v-carousel-item
    v-for="carousel in carousels"
    :src="carousel.image"
    cover
    ></v-carousel-item>

  </v-carousel>

  <v-carousel
      class="d-xs-flex d-md-none"
      height="250"
      cycle
      delimiter-icon="mdi-palette-outline"
  >

    <v-carousel-item
        v-for="carousel in carousels"
        :src="carousel.image"
        cover
    ></v-carousel-item>

  </v-carousel>

  <v-tabs
    v-model="tab"
    color="red"
    grow
  >
    <v-tab
      v-for="tab in tabs"
      :key="tab.title"
      :text="tab.title"
      :value="tab.title"
    ></v-tab>
  </v-tabs>

  <v-tabs-window v-model="tab">
    <v-tabs-window-item
      v-for="tab in tabs"
      :key="tab.title"
      :value="tab.title"
      >
        <v-card
          color="red-accent-1"
          flat
        >
          <v-card-text
            class="text-center text-white font-italic"
          >
            {{ tab.text }}</v-card-text>
        </v-card>
    </v-tabs-window-item>
    </v-tabs-window>

  <v-container
      class="hidden-sm-and-down"
      fluid>
    <v-row density="comfortable">
      <v-col
          v-for="page in pages"
          :key="page.title"
          :cols="page.flex">
        <v-hover
            v-slot="{ isHovering, props}"
        >
        <v-card
          :class="{ 'on-hover': isHovering }"
          :elevation="isHovering ? 12 : 2"
          v-bind="props"
        >
          <v-img
              :src="page.image"
              class="align-end"
              gradient="to top, rgba(1,1,1,.25), rgba(1,1,1,.25)"
              height="175"
              :aspect-ratio="16/9"
              cover
          >
            <v-card-title class="font-weight-bold text-center text-white mb-16">{{ page.title }}</v-card-title>

            <v-expand-transition>
              <div
                  v-if="isHovering"
                  class="d-md-flex bg-red-accent-1 v-card--reveal text-display-large"
                  style="height: 100%">
                <v-btn
                    color="grey-lighten-3"
                    :href="page.link"
                    prepend-icon="mdi-pencil-circle-outline"
                  >View Page</v-btn>
              </div>
            </v-expand-transition>

          </v-img>
          <v-card-subtitle
              class="text-center pa-4"
          >
            {{ page.subtitle }}
          </v-card-subtitle>
          </v-card>
        </v-hover>
      </v-col>
    </v-row>
  </v-container>

  <v-container
      class="d-xs-flex d-md-none"
      fluid
  >
    <v-row density="comfortable">
      <v-col
          v-for="page in pages"
          :key="page.title"
          :cols="page.flex">
          <v-card>
            <v-img
                :src="page.image"
                class="align-end"
                gradient="to top, rgba(1,1,1,.25), rgba(1,1,1,.25)"
                height="175"
                :aspect-ratio="16/9"
                cover
            >
              <v-card-title class="text-center text-white mb-16">{{ page.title }}</v-card-title>

            </v-img>
            <v-container>
              <v-row class="align-center justify-center flat">
                <v-btn
                    class="align-center justify-center v-btn--flat"
                    color="white"
                    :href="page.link"
                >View Page
                </v-btn>
              </v-row>
            </v-container>
          </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>
  .v-card--reveal {
    align-items: center;
    bottom: 0;
    justify-content: center;
    position: absolute;
    width: 100%;
  }
</style>