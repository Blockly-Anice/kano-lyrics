<template>
  <div class="rounded p-1">
    <div class="flex gap-2 text-amber-900 leading-6 rounded">

      <AccordionBar :title="titleFormat" :height="smBtnHeight" :bgColor="bgColor" :bgColorHover="bgColorHover">
        <div v-if="track.lyrics.romaji.timestamp">
          <br>
          <p v-html="track.lyrics.romaji.timestamp" class="text-base whitespace-pre-line"></p>
          <br>
          <p class="text-base whitespace-pre-line"><strong>Lyrics Source: </strong>
          <a :href="track.lyrics.romaji.source" target="_blank" class="underline decoration-amber-500 hover:decoration-amber-800 decoration-2">{{ track.lyrics.romaji.source }}</a></p>
          <p><strong>Syncronize by </strong>duke_w</p>
          <br>
        </div>
        <div v-else>
          <p>Unfortunately, I can't find the lyrics for this song 😞</p>
        </div>
      </AccordionBar>

      <TrackListButton @click="copiedToClipboard" :isDisabled="track.lyrics.romaji.timestamp"
      :height="smBtnHeight" :width="smBtnWidth" :bgColor="bgColor" :bgColorHover="bgColorHover" :message="'Copy'" :messageClicked="'Copied'">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" viewBox="0 0 20 20" fill="currentColor">
          <path d="M8 3a1 1 0 011-1h2a1 1 0 110 2H9a1 1 0 01-1-1z" />
          <path d="M6 3a2 2 0 00-2 2v11a2 2 0 002 2h8a2 2 0 002-2V5a2 2 0 00-2-2 3 3 0 01-3 3H9a3 3 0 01-3-3z" />
        </svg>
      </TrackListButton>

      <a :href="lrcFilePath" download>
        <TrackListButton :isDisabled="track.lyrics.romaji.timestamp"
        :height="smBtnHeight" :width="smBtnWidth" :bgColor="bgColor" :bgColorHover="bgColorHover" :message="'Download'" :messageClicked="'Downloaded'">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd"
              d="M3 17a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm3.293-7.707a1 1 0 011.414 0L9 10.586V3a1 1 0 112 0v7.586l1.293-1.293a1 1 0 111.414 1.414l-3 3a1 1 0 01-1.414 0l-3-3a1 1 0 010-1.414z"
              clip-rule="evenodd" />
          </svg>
        </TrackListButton>
      </a>

    </div>
  </div>
</template>

<script>
import TrackListButton from "./TrackListButton.vue";
import AccordionBar from "./AccordionBar.vue";

export default {
  data() {
    return {
      smBtnWidth: 'w-8',
      smBtnHeight: 'h-8',
      bgColor: 'bg-neutral-300/70',
      bgColorHover: 'hover:bg-neutral-100',
      titleFormat: `${this.track.id}. ${this.track.title.romaji}`,
      lrcFilePath: `/kano-lyrics/lyrics/${this.album}/${this.track.id}. ${this.track.title.romaji.replace('/', ' ')}.lrc`
    };
  },
  methods: {
    copiedToClipboard() {
      const songLyrics = this.track.lyrics.romaji.timestamp.replaceAll('<br>', '\n')
      navigator.clipboard.writeText(String(songLyrics))
    }
  },
  components: {
    AccordionBar,
    TrackListButton,
  },
  props: ['track', 'album'],
};
</script>