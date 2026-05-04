<script setup>
import PageHeader from "@/components/pageHeader.vue";
import ProjectCarousel from "@/components/projectCarousel.vue";
import {onMounted, ref} from "vue";

const tab = ref('Colored Pencil')
const styles = ref([])
const awards = ref([])
const commissions = ref([])
const loading = ref(true)
const error = ref('')

async function loadStyles() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('/api/styles')

    if (!response.ok) {
      throw new Error('Failed to load styles')
    }
    const data = await response.json();

    styles.value = data.map((style) => ({
      id: style.id,
      style: style.style,
      description: style.description,
      image_1: style.image_1,
      image_2: style.image_2,
      image_3: style.image_3
    }))
  } catch (err) {
    error.value = err.message || 'Error while trying to load styles'
  } finally {
    loading.value = false
  }
}

async function loadAwards() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('/api/awards')

    if (!response.ok) {
      throw new Error('Failed to load awards')
    }
    const data = await response.json();

    awards.value = data.map((award) => ({
      id: award.id,
      description: award.description
    }))
  } catch (err) {
    error.value = err.message || 'Error while trying to load awards'
  } finally {
    loading.value = false
  }
}

async function loadCommissions() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('/api/commissions')

    if (!response.ok) {
      throw new Error('Failed to load commissions')
    }
    const data = await response.json();

    commissions.value = data.map((commission) => ({
      id: commission.id,
      description: commission.description
    }))
  } catch (err) {
    error.value = err.message || 'Error while trying to load commission'
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  loadStyles()
  loadCommissions()
  loadAwards()
})
</script>

<template>
  <PageHeader title="About" description="Learn more about the different types of art"></PageHeader>

  <v-row>
    <v-col>
  <v-card>
    <v-tabs
        v-model="tab"
        color="white"
        class="bg-red-accent-1 text-grey-lighten-2"
        grow>
      <v-tab
          v-for="style in styles"
          :key="style.style"
          :text="style.style"
          :value="style.style"
      >
      </v-tab>
    </v-tabs>

    <v-tabs-window
        v-model="tab"
    >
      <v-tabs-window-item
          v-for="style in styles"
          :key="style.style"
          :value="style.style"
      >
        <ProjectCarousel
            :style="style.style"
            :description="style.description"
            :image_1="style.image_1"
            :image_2="style.image_2"
            :image_3="style.image_3"
        >
        </ProjectCarousel>
      </v-tabs-window-item>
    </v-tabs-window>
  </v-card>
    </v-col>
  </v-row>

  <v-row
  class="align-center justify-center"
  >
    <v-col
    cols="4"
    class="pl-2 pr-2 ms-2"
    >
      <v-card
          color="grey"
      >
        <v-card-title class="text-center">Past Commissions & Gifts</v-card-title>
        <v-card-text
            v-for="commission in commissions"
            :key="commission.id"
            class="text-center">{{commission.description}}</v-card-text>
      </v-card>
    </v-col>
    <v-col
        cols="4"
        class="pl-2 pr-2 ms-2"
    >
      <v-card
          color="grey"
      >
        <v-card-title class="text-center">Awards Won</v-card-title>
        <v-card-text
            v-for="award in awards"
            :key="award.id"
            class="text-center">{{award.description}}</v-card-text>
      </v-card>
    </v-col>
  </v-row>

</template>

<style scoped>

</style>