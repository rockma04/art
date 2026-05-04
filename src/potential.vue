<script setup>
import {onMounted, onUpdated, ref} from 'vue';
import PageHeader from "@/components/pageHeader.vue";
import ProjectCarousel from "@/components/projectCarousel.vue";

const textRule = ref([
    text => !!text || 'Field is required',
])

const dateRule = ref([
    date =>!!date || 'Date is required',
    date => (date && date.length === 16) || 'Format must be YYYY-MM-DD HH:MM',
])


const tab = ref('Colored Pencil')
const styles = ref([])
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

const calendar = ref([])
const events = ref ({
  name: '',
  start: '',
  end: ''
})

const list = ref([])
const items = ref ({
  style: '',
  project: '',
  item: ''
})


async function addEvent() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('http://localhost:3000/events',{
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(events.value),
    }).then(response => {
          if(response.ok) {
            window.location.reload();
          }
    });

    if(!response.ok) {
      throw new Error('Could not load event')
    }
  } catch (err) {
    error.value = err.message || 'Error while trying to load event'
  } finally {
    loading.value = false
  }
}

async function loadEvents() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('http://localhost:3000/calendar')

    if (!response.ok) {
      throw new Error('Failed to load calendar')
    }
    const data = await response.json();

    calendar.value = data.map((cal) => ({
      id: cal.id,
      name: cal.name,
      start: cal.start,
      end: cal.end
    }))
  } catch (err) {
    error.value = err.message || 'Error while trying to load calendar'
  } finally {
    loading.value = false
  }
}


async function addItem() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('http://localhost:3000/items',{
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(items.value),
    }).then(response => {
          if(response.ok) {
            window.location.reload();
          }
    });

    if(!response.ok) {
      throw new Error('Could not load list')
    }
  } catch (err) {
    error.value = err.message || 'Error while trying to load list'
  } finally {
    loading.value = false
  }
}

async function loadList() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('http://localhost:3000/stockList')

    if (!response.ok) {
      throw new Error('Failed to load list')
    }
    const data = await response.json();

    list.value = data.map((li) => ({
      id: li.id,
      style: li.style,
      project: li.project,
      item: li.item
    }))
  } catch (err) {
    error.value = err.message || 'Error while trying to load list'
  } finally {
    loading.value = false
  }
}

const color = ref("#000000")

onMounted(() => {
  loadStyles()
  loadList()
  loadEvents()
})

</script>

<template>
  <PageHeader title="Potential" description="Color Picker, Calendar, and Potential Projects"></PageHeader>

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

<v-container
  class="pt-4"
  cols="2"
>

  <v-row
      class=" pt-5 pb-2 align-center justify-center"
  >
    <h2
        class="header"
    >Project Schedule</h2>
  </v-row>

  <v-row>
    <v-col>
      <v-form
          class="header"
          @submit = "addEvent"
      >
        <v-text-field v-model="events.name" :rules="textRule" label="Event Name"></v-text-field>
        <v-text-field v-model="events.start" :rules="dateRule" label="Event Start"></v-text-field>
        <v-text-field v-model="events.end" :rules="dateRule" label="Event End"></v-text-field>

        <v-btn
            type="submit"
            color="red"
        >Submit</v-btn>
      </v-form>
    </v-col>
    <v-col
        class="hidden-sm-and-down"
    >
      <v-sheet
          height="550"
      >
        <v-calendar
            :events = "calendar"
            event-color="red"
            type="month"
            color="red"
        >
        </v-calendar>
      </v-sheet>
    </v-col>
    <v-col
        class="d-xs-flex d-md-none"
    >
      <v-sheet
          height="250"
      >
        <v-calendar
            :events = "calendar"
            event-color="red"
            type="4day"
            color="red"
        >
        </v-calendar>
      </v-sheet>
    </v-col>
  </v-row>
  <v-row
    class="pt-2 pb-2"
  >
  </v-row>

  <div>
  <v-divider
      color="grey-darken-1"
      thickness="2"
      class="pt-3 pb-2"
      gradient
  ></v-divider>
  </div>

  <v-row
    class=" pt-5 pb-2 align-center justify-center"
    >
    <h2
        class="header"
    >Project Ideas</h2>
  </v-row>

  <v-row>
    <v-col>
      <v-form
          @submit="addItem"
          class="header"
      >
        <v-text-field v-model="items.item" :rules="textRule" label="Item" required></v-text-field>
        <v-text-field v-model="items.style" :rules="textRule" label="Style" required></v-text-field>
        <v-text-field v-model="items.project" :rules="textRule" label="Project" required></v-text-field>

        <v-btn
            block
            color="red"
            type="submit"
        >Submit</v-btn>
      </v-form>
    </v-col>
  </v-row>
  <v-row>
  <v-col
      v-for="li in list"
      cols="4"
      class="pt-2 pb-8"
      :key="li.id">
    <v-card
    color="grey"
    >
      <v-card-title
      class="text-center text-wrap"
      >{{li.project}}</v-card-title>
      <v-card-subtitle
          class="text-center text-wrap"
      >{{li.style}}</v-card-subtitle>
      <v-card-text
          class="text-center text-wrap"
      >{{li.item}}</v-card-text>

    </v-card>
  </v-col>
  </v-row>

  <div>
    <v-divider
        color="grey-darken-1"
        thickness="2"
        class="pt-4 pb-2"
        gradient
    ></v-divider>
  </div>

  <v-row
      class=" pt-5 pb-2 align-center justify-center"
  >
    <h2
        class="header"
    >Color Workspace</h2>
  </v-row>

  <v-row
      class="pt-2 pb-2"
  >

    <v-col
    class="mb-2 pb-2"
    >
      <v-color-picker
          hide-inputs
          width="100%"
          dot-size = "15"
          class="align-content-center justify-center"
          v-model="color"
          :modes="['rgb']"
      ></v-color-picker>
    </v-col>
  </v-row>
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