<template>
  <!-- CARD -->
  <div @click="toggleOverlay"
    class="flex flex-row lg:flex-col items-center lg:items-start z-10 p-2 hover:bg-gray-100 bg-amber-50/60 rounded shadow-lg cursor-pointer duration-300 lg:p-4">
    <img v-bind:src="'/kano-lyrics/album_cover/' + album.cover" class="object-cover w-24 h-24 lg:w-full lg:h-56 rounded"
      alt="" />

    <div class="ml-3 lg:ml-0">
      <h3 class="font-bold pt-3">
        {{ album.title.romaji }}
      </h3>
      <small>Released on {{ album.released }}</small>
    </div>

  </div>

  <!-- EXIT OVERLAY -->
  <div v-show="exiting" class="fixed inset-0 z-30 rounded drop-shadow-lg bg-fixed bg-center bg-cover animate-zoom-in bg-[url('/src/assets/banner.webp')]"></div>

  <!-- OVERLAY -->
  <div v-show="overlay"
        class="fixed inset-0 z-20 rounded drop-shadow-lg bg-fixed bg-center bg-cover animate-zoom-out bg-[url('/src/assets/banner.webp')]">
    <div class="relative w-auto mx-auto max-w-6xl h-full bg-neutral-50/30">

      <!-- CLOSE BUTTON -->
      <button @click="exitOverlay" class="fixed right-0 z-20 p-2 m-4 bg-neutral-50/40 hover:bg-neutral-50/80 rounded-full">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"
          stroke-width="2">
          <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>

      <!-- CONTENT -->
      <div class="flex flex-wrap overflow-y-scroll h-screen">
        <div class="w-full">
          <div class="relative flex flex-col min-w-0 mb-6 rounded">
            <div class="px-4 py-5 flex-auto">
                <div v-for="album in albums" :key="album.id" :class="{'hidden': openTab !== album.id, 'block': openTab === album.id}">

                  <albumHeader :album="album" />
                  <trackList v-for="track in album.tracklist" :key="track.id" :track="track" :album="album.title.romaji"/>

                </div>
            </div>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import trackList from "./TrackList.vue";
import albumHeader from "./AlbumHeader.vue";

export default {
  data() {
    return {
      overlay: false,
      exiting: false,
      openTab: this.getOpenTab,
    }
  },
  methods: {
    toggleOverlay() {
      this.overlay = !this.overlay
      const body = document.getElementsByTagName('body')[0]
      body.classList.add("overflow-hidden")
    },
    exitOverlay() {
      this.overlay = !this.overlay
      this.exiting = !this.exiting

      const body = document.getElementsByTagName('body')[0]
      body.classList.remove("overflow-hidden")

      setTimeout(() => this.exiting = false, 500);
    },
    toggleTabs: function(tabNumber){
      this.openTab = tabNumber
    }
  },
  components: {
    trackList,
    albumHeader,
  },
  props: ['albums', 'album', 'getOpenTab'],
};
</script>