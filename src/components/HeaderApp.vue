<script lang="ts">
export default {
  props: [],
  methods: {},
};
</script>
<script setup lang="ts">
import Swal from "sweetalert2";

const onShowInfo = () => {
  Swal.fire({
    title: "info",
    text: "Do you want to continue",
    icon: "info",
    confirmButtonText: "OK",
    footer: "Author",
  });
};
</script>
<template>
  <div class="fixed top-0 z-10 navbar bg-base-300">
    <div class="flex-1">
      <a class="logo-font btn btn-ghost normal-case text-2xl">MyGallery</a>
    </div>
    <div class="flex-none">
      <button @click="onShowInfo" class="btn btn-square btn-ghost">
        <i class="fa-solid text-info fa-circle-question fa-2xl"></i>
      </button>
    </div>
  </div>
</template>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Lobster&family=Nanum+Gothic&family=Roboto:wght@500&display=swap");
.logo-font {
  font-family: "Lobster", cursive;
}
</style>
