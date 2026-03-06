<script setup>
const props = defineProps({
  title: {type: String, required: true},
  description: {type: String, required: true}
})
</script>

<template>
  <v-sheet
    class="align-center justify center"
    >
  <div>
    <h1 class="header pt-8 text-red text-center">{{ title }}</h1>
  </div>
  <div>
    <h3 class="header text-grey-darken-1 pt-3 pb-4 text-center">{{ description }}</h3>
  </div>
  <div>
    <v-divider
      color="grey-darken-1"
      thickness="2"
      class="pt-3 pb-2"
      gradient
    ></v-divider>
  </div>
  </v-sheet>
</template>

<style scoped>
.header {
  font-family: "Manrope", sans-serif;
  font-weight: 400;
  font-style: normal;
  line-height: 1.5;
}
</style>