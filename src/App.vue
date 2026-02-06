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

window.addEventListener('hashchange', ()=> {
  currentPath.value = window.location.hash
})
const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/']  || NotFound
})
</script>

<template>
  <a href="#/">Home</a> |
  <a href="#/about">About</a> |
  <a href="#/stock">Stock</a> |
  <a href="#/completed">Completed</a> |
  <a href="#/potential">Potential</a> |

  <component :is="currentView"></component>
</template>

