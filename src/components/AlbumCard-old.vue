<template>
  <!-- Card -->
  <div @click="toggleOverlay" class="flex flex-row lg:flex-col p-4 hover:bg-gray-100 bg-amber-50/60 rounded shadow-lg cursor-pointer duration-300">
    <img v-bind:src="'/album_cover/' + track.cover" class="object-cover w-full h-56 rounded" alt="" />

    <div class="font-bold pt-3">
      {{ track.album_title }}
    </div>
    <small>Released on {{ track.released }}</small>
  </div>

  <!-- <div v-if="overlay" class="fixed inset-0 rounded shadow-lg items-center bg-fixed bg-center bg-cover" style="background-image: url('/src/assets/cover.jpg');"> -->
  <div v-if="overlay" class="fixed inset-0 rounded shadow-lg items-center bg-fixed bg-center bg-cover" v-bind:style="{ 'background-image': `url(/src/assets/album_cover/${track.cover})`}">
    <div class="relative w-auto mx-auto max-w-6xl bg-neutral-50/50 h-full">
      <button @click="toggleOverlay" class="p-2 bg-blue-100">
        X
      </button>

      <div class="flex flex-wrap z-50">
        <div class="w-full">

          <!-- ALBUM BAR -->
          <ul class="flex mb-0 list-none flex-wrap pt-3 pb-4 flex-row justify-center gap-2">
            <li v-for="track in tracks" :key="track.id" class="text-center cursor-pointer">
              <img v-bind:src="'/src/assets/album_cover/' + track.cover" class="object-cover h-16 w-16 rounded p-1" alt=""
                v-on:click="toggleTabs(track.id)"
                v-bind:class="{'text-pink-600 bg-white': openTab !== track.id, 'text-white bg-pink-600': openTab === track.id}" />
            </li>
          </ul>

          <div class="relative flex flex-col min-w-0 break-words mb-6 rounded">
            <div class="px-4 py-5 flex-auto">

              <div class="tab-content tab-space overflow-Y-scroll max-h-screen">
                <div v-for="track in tracks" :key="track.id" v-bind:class="{'hidden': openTab !== track.id, 'block': openTab === track.id}">
                  <div>
                    <img v-bind:src="'/src/assets/album_cover/' + track.cover" class="object-cover w-56 h-56 rounded" alt="" />
                    <h1 class="text-xl font-bold">{{ track.album_title }}</h1>
                  </div>
                  <tracklist v-for="song in track.tracklist" :key="song.id" :id="song.id" :title="song.title" :misc="song.misc"/>
                </div>
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

export default {
  data() {
    return {
      overlay: false,
      openTab: this.getOpenTab
    }
  },
  methods: {
    toggleOverlay() {
      this.overlay = !this.overlay
      this.openTab = this.openTab
    },
    toggleTabs: function(tabNumber){
      this.openTab = tabNumber
    }
  },
  components: {
    tracklist: trackList,
  },
  props: ['tracks', 'track', 'getOpenTab'],
};
</script>