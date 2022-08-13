<template>
    <div class="flex flex-nowrap px-1 py-5 items-end">
        <img v-bind:src="'/album_cover/' + album.cover" class="object-cover w-24 h-24 lg:w-56 lg:h-56 rounded" alt="" />
        <div class="p-3 md:p-5">
          <h1 class="text-2xl lg:text-5xl font-bold">{{ album.title.romaji }}</h1>
          <h3 class="md:pt-2">{{ album.released }}</h3>
        </div>
    </div>
</template>

<script>
export default {
  props: ['album'],
};
</script>