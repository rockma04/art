<script setup>
import { ref } from 'vue'

const reveal = ref(false)

const props = defineProps({
  style: {type: String, required: true},
  description: {type: String, required: true},
  image_1: {type: String, default: ''},
  image_2: {type: String, default: ''},
  image_3: {type: String, default: ''},
  link: {type: String, default: ''}
})
</script>

<template>
  <v-card
      color="grey-lighten-2"
      class="text-red"
  >
    <v-card-text
      class="pl-10 pr-10 text-subtitle-1"
    >
      {{ description }}
    </v-card-text>

    <v-btn
        class="pl-10 pr-10 pb-5 text-subtitle-1"
        variant="text"
        text="View Examples"
        @click="reveal = true"
    >
    </v-btn>

    <v-dialog
        v-model="reveal"
    >
      <v-carousel
          height="450"
          show-arrows="hover"
          delimiter-icon="mdi-palette-outline"
      >
        <v-carousel-item
            :src="image_1"
        >
        </v-carousel-item>
        <v-carousel-item
            :src="image_2"
        >
        </v-carousel-item>
        <v-carousel-item
            :src="image_3"
        >
        </v-carousel-item>
      </v-carousel>

      <v-btn
          variant="text"
          class="align-center pt-2 pb-2"
          color="white"
          text="close"
          @click="reveal = false"
      >
      </v-btn>
    </v-dialog>
  </v-card>
</template>

<style scoped>
</style>