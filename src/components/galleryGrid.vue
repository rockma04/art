<script setup>
  import { ref } from 'vue'

  const props = defineProps({
    description: {type: String, required: true},
    image: {type: String, default: '', required: true},
    completed: {type: String, default: '', required: true}
  })
</script>

<template>
  <v-container
      class="hidden-sm-and-down pa-2"
  >
  <v-img
      height="350"
      aspect-ratio="16/9"
      :src="image"
  >
  </v-img>
    <p
    class="pt-1 text-center header"
    >{{description}}</p>
    <p
        class="pt-0 text-center header"
    >{{completed}}</p>
  </v-container>

  <v-container
      class="d-xs-flex d-md-none pa-2"
      fluid
  >
  <v-img
      height="150"
      :src="image"
  ></v-img>
  <p
      class="pt-1 text-center header"
  >{{description}}
  </p>
  </v-container>

</template>

<style scoped>
.header {
  font-family: "Manrope", sans-serif;
  font-weight: 400;
  font-style: normal;
  line-height: 1;
}
</style>