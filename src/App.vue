<script lang="ts">
import { createClient, Photos, ErrorResponse, Photo } from "pexels";
import axios from "axios";

const client = createClient(
  "iIEcsydd2RFNuQPxnzhMalDlMMMxn0GGGpxM0vFq3b9snNlSSLm12ShI"
);
const pexelApi = "https://api.pexels.com/v1/curated?page=1&per_page=40";

export default {
  data() {
    return {
      onLoading: true,
      pexelPhotos: <Photo[]>[],
    };
  },
  async mounted() {
    this.loadedPhotos();
  },
  methods: {
    loadedPhotos() {
      (this.pexelPhotos = <Photo[]>[]), (this.onLoading = true);
      client.photos
        .curated({ per_page: 9, page: Math.floor(Math.random() * 20) + 1 })
        .then((res) => {
          this.pexelPhotos = <Photo[]>res.photos;
          this.onLoading = false;
        })
        .catch((err) => {
          console.error(err);
        });
    },
  },
};
</script>

<script setup lang="ts">
import HeaderApp from "./components/HeaderApp.vue";
import ArtboardComponent from "./components/ArtboradComponent.vue";
import LoadingComponent from "./components/LoadingComponent.vue";
</script>

<template>
  <header>
    <HeaderApp></HeaderApp>
    <template> </template>
  </header>
  <main>
    <div class="container mx-auto">
      <div
        v-if="onLoading === true"
        class="h-screen flex justify-center items-center"
      >
        <LoadingComponent></LoadingComponent>
      </div>
      <div v-else>
        <div class="grid grid-flow-row-dense grid-cols-3 gap-3 my-20">
          <div v-for="photo in pexelPhotos">
            <ArtboardComponent
              :photo-height="photo.height"
              :photo-width="photo.width"
              :img-src="photo.src.original"
              :img-url="photo.url"
              :photograph-author="photo.photographer"
            ></ArtboardComponent>
          </div>
        </div>
        <div class="flex justify-center">
          <div
            @click="loadedPhotos"
            class="animate-bounce h-16 mb-10 flex justify-center items-center"
          >
            <h2
              class="badge bg-primary hover:bg-primary-focus badge-lg p-6 uppercase cursor-pointer"
            >
              Random Images
            </h2>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped></style>
