<script lang="ts">
export default {
  props: {
    imgSrc: String,
    photographAuthor: String,
    photoWidth: Number,
    photoHeight: Number,
    imgUrl: String,
  },
};
</script>
<script setup lang="ts">
import { ref } from "vue";
import LoadingComponent from "./LoadingComponent.vue";

const count = {
  likes: ref(0),
  dislikes: ref(0),
};
</script>
<template>
  <div v-if="imgSrc === ''" class="animate-pulse artboard artboard-demo">
    <LoadingComponent></LoadingComponent>
    <template> </template>
  </div>
  <div
    v-else
    class="group/card hovering-artborad shadow-md duration-300 artboard artboard-demo rounded-lg bg-base-300"
  >
    <div :class="`h-[${photoHeight}px]`" class="group relative w-full">
      <div
        id="icon"
        class="absolute invisible group-hover/card:visible flex right-2 flex-col gap-2 text-dark top-2"
      >
        <div class="grid grid-cols-2 place-self-center gap-2">
          <div
            @click="count.likes.value++"
            class="icon-hover bg-base-200 flex flex-col justify-center items-center gap-2 !opacity-100 rounded-lg h-10 w-10"
          >
            <i class="fa fa-regular fa-heart fa-lg mt-2"></i>
            <div class="badge badge-xs p-0.5 badge-secondary -mt-0.5">
              +{{ count.likes }}
            </div>
          </div>
          <div
            @click="count.dislikes.value++"
            class="icon-hover bg-base-200 flex flex-col justify-center items-center gap-2 !opacity-100 rounded-lg h-10 w-10"
          >
            <i class="fa-solid fa-heart-crack fa-lg mt-2"></i>
            <div class="badge badge-xs p-0.5 -mt-0.5">
              +{{ count.dislikes }}
            </div>
          </div>
        </div>
        <div
          class="flex gap-1 justify-self-end text-[11px] badge badge-accent font-semibold text-white"
        >
          <i class="fa-solid fa-user fa-xs"></i>
          {{ photographAuthor }}
        </div>
      </div>
    </div>
    <a :href="imgUrl" target="_blank" class="cursor-zoom-in">
      <img :src="imgSrc" alt="" class="h-full w-full rounded-lg" />
    </a>
  </div>
</template>
<style scoped>
@tailwind components;

@layer components {
  .hovering-artborad:hover {
    @apply opacity-90 shadow-lg drop-shadow-lg duration-300 cursor-zoom-in;
  }

  .icon-hover:hover {
    @apply !opacity-100 duration-500 shadow-lg cursor-pointer;
  }
}
</style>
