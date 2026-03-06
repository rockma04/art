<script setup>
import { ref, computed } from 'vue'
import home from './home.vue'
import about from './about.vue'
import stock from './stock.vue'
import potential from './potential.vue'
import completed from './completed.vue'
import photo from './photoGallery.vue'
import print from './printGallery.vue'
import pencil from './pencilGallery.vue'

const routes = {
  '/': home,
  '/about': about,
  '/stock': stock,
  '/potential': potential,
  '/completed': completed,
  '/photo': photo,
  '/print': print,
  '/pencil': pencil,

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
        class="text-grey-lighten-5 header"
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
          @click="drawer = !drawer"
      ></v-list-item>
      <v-list-item
          prepend-icon="mdi-list-box-outline"
          href="#/stock"
          title="Stock"
          @click="drawer = !drawer"
      ></v-list-item>
      <v-list-item
          prepend-icon="mdi-lightbulb-on-outline"
          href="#/potential"
          title="Potential"
          @click="drawer = !drawer"
      ></v-list-item>
      <v-list-item
          prepend-icon="mdi-check-outline"
          href="#/completed"
          title="Completed"
          @click="drawer = !drawer"
      ></v-list-item>
    </v-navigation-drawer>
    <v-app-bar
        color="red"
        class="text-white"
        scroll-behavior="collapse"
    >
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-btn
          href="#/">
        <v-app-bar-title class="text-h4 header">
          The Working Title
        </v-app-bar-title>
      </v-btn>
    </v-app-bar>
    <v-main>
      <component :is="currentView"></component>
    </v-main>
    <v-footer class="absolute app=false justify-center">Copyright 2026</v-footer>
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

