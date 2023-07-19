<script setup>
// import tracksData from "./assets/kano_discography.json";
import tracksData from "./assets/kano_discography_new.json";
// Components
import copiedAlert from "./components/CopiedAlert.vue";
import albumCard from "./components/AlbumCard.vue";
import tabNav from "./components/TabsNav.vue";
import AlertPop from "./components/AlertPopUp.vue"
</script>

<template>
  <AlertPop/>

  <div class="px-4 py-16 mx-auto sm:max-w-xl md:max-w-full lg:max-w-screen-xl md:px-24 lg:px-8 lg:py-20">
    <div class="max-w-xl mb-10 md:mx-auto sm:text-center lg:max-w-2xl md:mb-12 mt-[35vh]">
      <div>
        <p
          class="inline-block px-3 py-px mb-4 text-xs font-semibold tracking-wider uppercase rounded-full">
          Kano Lyrics Repository
        </p>
      </div>
      <h2
        class="max-w-lg mb-6 font-sans text-3xl font-bold leading-none tracking-tight text-gray-900 sm:text-4xl md:mx-auto">
        <span class="relative inline-block">
          <svg viewBox="0 0 52 24" fill="currentColor"
            class="absolute top-0 left-0 z-0 hidden w-32 -mt-8 -ml-20 text-blue-gray-100 lg:w-32 lg:-ml-28 lg:-mt-10 sm:block">
            <defs>
              <pattern id="9a29985a-fc16-419b-ae53-1670f5ca4491" x="0" y="0" width=".135" height=".30">
                <circle cx="1" cy="1" r=".7"></circle>
              </pattern>
            </defs>
            <rect fill="url(#9a29985a-fc16-419b-ae53-1670f5ca4491)" width="52" height="24"></rect>
          </svg>
          <span class="relative">鹿乃 | </span>
        </span>
        歌う人。音楽ユニット
      </h2>
      <p class="text-base md:text-lg">
        Kano (Japanese: 鹿乃, born December 24) is a Japanese musician and virtual YouTuber who is signed to Imperial Records. She began her artist activities as a doujin artist, uploading songs on the video-sharing website Nicovideo.
      </p>
    </div>

    <div class="grid max-w-screen-lg gap-2 lg:gap-8 row-gap-5 mb-8 sm:grid-cols-2 lg:grid-cols-4 sm:mx-auto">
      <albumCard v-for="album in albums" :key="album.id" :albums="albums" :album="album" :getOpenTab="album.id"/>
    </div>

    <div class="flex items-center sm:justify-center">
      <a href="https://github.com/wahyukusumo/kano-lyrics"
        class="flex items-center justify-center h-12 px-6 mr-6 font-medium tracking-wide text-white transition duration-200 rounded">
        Github
      </a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      albums: tracksData,
    };
  },
  components: {
    alert: copiedAlert,
    card: albumCard,
    tabnav: tabNav,
    AlertPop: AlertPop,
  }
};
</script>
