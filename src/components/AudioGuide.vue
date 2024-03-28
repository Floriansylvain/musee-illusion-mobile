<script setup lang="ts">
import { ref } from "vue";
import { IonIcon } from "@ionic/vue";
import {
  playCircle as playIcon,
  pauseCircle as pauseIcon,
} from "ionicons/icons";

const props = defineProps<{
  src: string;
}>();

const audioRef = ref<HTMLAudioElement | null>(null);
const isPlaying = ref(false);

const toggleAudio = () => {
  if (audioRef.value?.paused) {
    audioRef.value?.play();
  } else {
    audioRef.value?.pause();
  }
  isPlaying.value = !audioRef.value?.paused;
};
</script>

<template>
  <audio preload="auto" ref="audioRef" :src="props.src"></audio>
  <article class="audio-guide">
    <button type="button" @click="toggleAudio">
      <ion-icon :icon="isPlaying ? pauseIcon : playIcon"></ion-icon>
    </button>
    <aside>
      <h5>AUDIO GUIDE</h5>
      <p>uwu uwu uwu uwu uwu uwu uwu uwu uwu</p>
    </aside>
  </article>
</template>

<style scoped>
.audio-guide {
  display: flex;
  gap: 8px;

  padding: 8px;

  color: var(--ion-color-light-tint);
  background-color: var(--ion-color-dark);

  border-radius: 8px;
}

.audio-guide button {
  display: flex;
  justify-content: center;
  align-items: center;

  background: none;
  border: none;
  outline: none;
}

.audio-guide ion-icon {
  width: 43px;
  height: 43px;
  fill: var(--ion-color-light-tint);
}

.audio-guide p {
  margin: 0;
}

h5 {
  font-size: 16px;
  font-weight: bold;
  margin: 0;
}
</style>
