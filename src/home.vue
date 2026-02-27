<script setup>
  import { ref } from 'vue'

  const tab = ref(null)

  const values = [
    {
      title: 'Types',
      image: 'types.jpeg',
      text: 'Photographs, prints, paintings, drawings. There are many types of art which you can learn more about or see different completed projects throughout the sections below. '
    },
    {
      title: 'Materials',
      image: 'materials.JPG',
      text: 'Colored pencils, paint, ink. Check out the types of materials used in different projects and keep track of what is still available on the stock page. ',
    },
  ]

  const pages = [
    {
      title: 'About',
      subtitle: 'Learn more about the different types of art!',
      image: 'about.jpeg',
      link: '#/about',
      flex: 12
    },
    {
      title: 'Stock',
      subtitle: 'Check out what items are currently available!',
      image: 'stock.jpeg',
      link: '#/stock',
      flex: 4
    },
    {
      title: 'Potential',
      subtitle: 'Look through possible projects to complete!',
      image: 'potential.jpeg',
      link: '#/potential',
      flex: 4
    },
    {
      title: 'Completed',
      subtitle: 'View the completed projects!',
      image: 'completed.jpeg',
      link: '#/completed',
      flex: 4
    },
  ]
</script>

<template>
  <v-carousel
      height="675"
      cycle
      delimiter-icon="mdi-palette-outline"
  >

    <v-carousel-item>
      <v-parallax
          src="materials.JPG">
      </v-parallax>
    </v-carousel-item>

    <v-carousel-item>
      <v-parallax
          src="carousel_3.jpeg">
      </v-parallax>
    </v-carousel-item>

    <v-carousel-item>
      <v-parallax
          src="completed.jpeg">
      </v-parallax>
    </v-carousel-item>

    <v-carousel-item>
      <v-parallax
          src="carousel_8.JPG">
      </v-parallax>
    </v-carousel-item>
  </v-carousel>

  <v-tabs
    v-model="tab"
    color="red"
    grow
  >
    <v-tab
      v-for="value in values"
      :key="value.title"
      :text="value.title"
      :value="value.title"
    ></v-tab>
  </v-tabs>

  <v-tabs-window v-model="tab">
    <v-tabs-window-item
      v-for="value in values"
      :key="value.title"
      :value="value.title"
      >
        <v-card
          color="red-accent-1"
          flat
        >
          <v-card-text
            class="text-center text-white font-italic"
          >
            {{ value.text }}</v-card-text>
        </v-card>
    </v-tabs-window-item>
    </v-tabs-window>

  <v-container fluid>
    <v-row density="comfortable">
      <v-col
          v-for="page in pages"
          :key="page.title"
          :cols="page.flex">
        <v-hover v-slot="{ isHovering, props}">
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
                  class="d-flex bg-red-accent-1 v-card--reveal text-display-large"
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
          >{{ page.subtitle }}</v-card-subtitle>

          </v-card>
        </v-hover>
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