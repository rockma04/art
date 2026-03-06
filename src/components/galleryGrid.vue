<script setup>
  import { ref } from 'vue'

  const props = defineProps({
    description: {type: String, required: true},
    image: {type: String, default: '', required: true},
  })
</script>

<template>
  <v-img
      class="pa-2"
      height="450"
    :src="image"
  ></v-img>

</template>

<style scoped>

</style>