<script setup>
  import {ref} from "vue"
  import PageHeader from "./components/pageHeader.vue"

  const galleries = [
    {
      style: 'Colored Pencil',
      description: 'Landscapes, Portraits, Nature, and Still Lives.',
      link: '#/pencil'
    },
    {
      style: 'Collage',
      description: 'Landscapes, Portraits, Nature, and Still Lives.',
      link: '#/pencil'
    },
    {
      style: 'Painting',
      description: 'Landscapes, Portraits, Nature, and Still Lives.',
      link: '#/pencil'
    },
    {
      style: 'Photography',
      description: 'Landscapes, Portraits, Nature, and Still Lives.',
      link: '#/photo'
    },
    {
      style: 'Prints',
      description: 'Landscapes, Portraits, Nature, and Still Lives.',
      link: '#/print'
    },
    {
      style: 'Other',
      description: 'Landscapes, Portraits, Nature, and Still Lives.',
      link: '#/pencil'
    }
  ]
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