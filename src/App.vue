<script setup>
import { ref, computed } from 'vue'
import home from './home.vue'
import about from './about.vue'
import stock from './stock.vue'
import completed from './completed.vue'
import potential from './potential.vue'

const routes = {
  '/': home,
  '/about': about,
  '/stock': stock,
  '/completed': completed,
  '/potential': potential
}

const currentPath = ref (window.location.hash)
const drawer = ref(false)

window.addEventListener('hashchange', ()=> {
  currentPath.value = window.location.hash
})
const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/']  || NotFound
})
</script>

<template>
  <v-app>
    <v-navigation-drawer
        color="red-accent-1"
        class="text-grey-lighten-5"
        v-model="drawer">
      <v-list-item
          prepend-icon="mdi-home-outline"
          href="#/"
          title="Home"
          @click="drawer =! drawer"
      ></v-list-item>
      <v-list-item
          prepend-icon="mdi-information-outline"
          href="#/about"
          title="About"
          @click="drawer =! drawer"
      ></v-list-item>
      <v-list-item
          prepend-icon="mdi-list-box-outline"
          href="#/stock"
          title="Stock"
          @click="drawer =! drawer"
      ></v-list-item>
      <v-list-item
          prepend-icon="mdi-check-outline"
          href="#/completed"
          title="Completed"
          @click="drawer =! drawer"
      ></v-list-item>
      <v-list-item
          prepend-icon="mdi-lightbulb-on-outline"
          href="#/potential"
          title="Potential"
          @click="drawer =! drawer"
      ></v-list-item>
    </v-navigation-drawer>
    <v-app-bar
        color="red"
        class="text-white"
        scroll-behavior="collapse"
    >
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-app-bar-title class="text-h3 header">The Working Title</v-app-bar-title>
    </v-app-bar>
    <v-main>
      <component :is="currentView"></component>
    </v-main>
    <v-footer app="true">Copyright 2026</v-footer>
  </v-app>
</template>

<style scoped>
  .header {
    font-family: "Manrope", sans-serif;
    font-weight: 200;
    font-style: normal;
    line-height: 1.5;
  }
</style>

