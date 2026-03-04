<script setup>
import { ref } from 'vue'

const reveal = ref(false)

  const props = defineProps({
    style: {type: String, required: true},
    description: {type: String, required: true},
    image: {type: String, default: ''},
    link: {type: String, default: ''}
  })
</script>

<template>
      <v-card>
        <v-img
          :src="image"
          cover
        >
          <v-card-title>{{ style }}</v-card-title>
        </v-img>

        <v-card-actions>
          <v-btn
            text="More"
            @click="reveal = true"
          ></v-btn>
        </v-card-actions>

        <v-expand-transition>
          <v-card
            v-if="reveal"
            height="100%">
            <v-card-text>
              {{ description }}
            </v-card-text>
          </v-card>
        </v-expand-transition>
      </v-card>
</template>

<style scoped>

</style>