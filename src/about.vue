<script setup>
  import {ref} from "vue"
  import PageHeader from "./components/pageHeader.vue"
  import ProjectCarousel from "./components/projectCarousel.vue"

  const tab = ref('Colored Pencil')

  const projects = [
    {
      style: 'Colored Pencil',
      description: 'Colored Pencil allows for the artist to work in detail and to add details that may be more difficult with other mediums. ' +
          'With a quality set of colored pencils, the artist is able to blend the colors to show the shadows and curves of different fabrics or textures in detail.' +
          '',
      image_1: 'cp_1.jpg',
      image_2: 'completed.jpg',
      image_3: 'completed.jpg',
    },
    {
      style: 'Painting',
      description: 'There are many types of paint that an artist can choose from, including: Acrylic, Oils, or Watercolors. ' +
          'Acrylic paints are quick to dry while oil paints are slower and allow more time to mix. ' +
          'Watercolors are a lighter color and can be used in several ways ranging from subtle tints of color, to full coverage in paintings.',
      image_1: 'painting_1.JPG',
      image_2: 'painting_2.jpg',
      image_3: 'completed.jpg',
    },
    {
      style: 'Photography',
      description: 'Landscapes, Portraits, Nature, and Still Lives. Photography offers the artist the ability to capture a moment in time whether that be a sunset over a lake' +
          ', a portrait of a friend, or an artistic framing of a common everyday object. Camera types can range from cellphones to digital cameras to vintage film cameras. ' +
          'Each camera will offer its own unique perspective on the photo taken.',
      image_1: 'photo_17.jpg',
      image_2: 'photo_12.jpg',
      image_3: 'photo_18.jpg',
    },
    {
      style: 'Prints',
      description: 'Prints offer offer a wide variety of styles an artist could choose from including, monoprints, etching, relief prints, or image transfers. While relief prints ' +
          'require the artist to shave away at the base material and stamp a new layer on one at a time, an etching will provide them the opportunity to etch into the protective layer added over their' +
          'metal base and use a chemical process to create the idents from their etching to eventually print the image they are intending to create.',
      image_1: 'print_1.jpg',
      image_2: 'print_8.jpg',
      image_3: 'print_18.jpg',
    },
    {
      style: 'Other',
      description: 'Art can be found in many different places aside from the previous mediums mentioned. Art can be created through collages, digitally, fabrics, markers, pencils, and many other materials.',
      image_1: 'dress_1.jpg',
      image_2: 'dress_2.jpg',
      image_3: 'dress_3.jpg'
    }
  ]
</script>

<template>
  <PageHeader title="Learn About Us!" description="Interested in learning more about the different styles of art? Check out the different styles below or learn more about the process below."></PageHeader>


  <v-card>
  <v-tabs
      v-model="tab"
      color="white"
      class="bg-red-accent-1 text-grey-lighten-2"
    grow>
    <v-tab
      v-for="pro in projects"
      :key="pro.style"
      :text="pro.style"
      :value="pro.style"
      >
    </v-tab>
  </v-tabs>

  <v-tabs-window
      v-model="tab"
  >
    <v-tabs-window-item
      v-for="pro in projects"
      :key="pro.style"
      :value="pro.style"
    >
        <ProjectCarousel
          :style="pro.style"
          :description="pro.description"
          :image_1="pro.image_1"
          :image_2="pro.image_2"
          :image_3="pro.image_3"
        >
        </ProjectCarousel>
      </v-tabs-window-item>
    </v-tabs-window>
  </v-card>

  <v-divider></v-divider>

  <v-timeline
      class="pa-5"
      direction="horizontal"
      align="start">
    <v-timeline-item
        dot-color="grey"
        size="small"
    >
      <template v-slot:opposite
      >
        <p class="header text-grey-darken-1">Beginning</p>
      </template>
      <v-card
          class="bg-red-accent-1"
      >
        <v-card-text
          class="text-center text-white"
        >
          The start of a project! <br>
          When you start with an idea<br>
          of what you would like to create <br>
          and begin to get things ready. <br>
        </v-card-text>
      </v-card>
    </v-timeline-item>

    <v-timeline-item
        dot-color="grey"
        size="small"
    >
      <template v-slot:opposite>
        <p class="header text-grey-darken-1">Drafting</p>
      </template>
      <v-card
          class="bg-red-accent-1"
      >
        <v-card-text
          class="text-center text-white"
        >With the idea, you move on to figuring <br>
        out how you would like to make it happen. <br>
        You could sketch if you are drawing or test <br>
        settings for your camera.</v-card-text>
      </v-card>
    </v-timeline-item>

    <v-timeline-item
        dot-color="grey"
        size="small"
    >
      <template v-slot:opposite>
        <p class="header text-grey-darken-1">Next steps</p>
      </template>
      <v-card
          class="bg-red-accent-1"
      >
        <v-card-text
            class="text-center text-white"
        >
          As you are working on a project <br>
          you may have changes, edits, or <br>
          tools that you need to adjust for. <br>
          Adapting and adjusting your idea as <br>
          you work is important!
        </v-card-text>
      </v-card>
    </v-timeline-item>

    <v-timeline-item
        dot-color="grey"
        size="small"
    >
      <template v-slot:opposite>
        <p class="header text-grey-darken-1">Final Touches</p>
      </template>
      <v-card
          class="bg-red-accent-1"
      >
        <v-card-text
          class="text-center text-white"
        >Finishing the project gives the <br>
        opportunity to present your work to <br>
        other or to put it on display. <br>
        The presentation of the final work <br>
        can pull the whole piece together.</v-card-text>
      </v-card>
    </v-timeline-item>
  </v-timeline>
</template>

<style scoped>

  .header {
    font-family: "Manrope", sans-serif;
    font-weight: 200;
    font-style: normal;
    line-height: 1.5;
  }
</style>