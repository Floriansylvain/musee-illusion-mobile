<script setup lang="ts">
import { ref } from "vue";
import { Pagination, EffectCoverflow } from "swiper/modules";
import { Swiper, SwiperSlide } from "swiper/vue";

import AudioGuide from "@/components/AudioGuide.vue";

import "swiper/css";
import "swiper/css/effect-coverflow";

const props = defineProps<{
  data: any;
}>();

const pagination = ref<HTMLElement | null>(null);

defineEmits(["onSlideIndexChange"]);
</script>

<template>
  <swiper
    :pagination="{
      clickable: true,
      el: pagination,
      bulletClass: 'pagination-bullet',
      bulletActiveClass: 'pagination-bullet-active',
    }"
    :modules="[Pagination, EffectCoverflow]"
    :space-between="250"
    :auto-height="false"
    @slide-change-transition-end="
      (e) => $emit('onSlideIndexChange', e.activeIndex)
    "
    class="swiper-horizontal"
    effect="coverflow"
    :coverflowEffect="{
      rotate: 50,
      stretch: 0,
      depth: 100,
      modifier: 1,
      slideShadows: false,
    }"
  >
    <swiper-slide v-for="element in props.data" :key="element.titre">
      <section>
        <h4>{{ element.fields.titre }}</h4>
        <img :src="element.fields.image[0].url" alt="hallan" />
        <AudioGuide :src="element.fields.audio[0].url" />
      </section>
    </swiper-slide>
  </swiper>
  <div ref="pagination" slot="pagination" class="swiper-pagination"></div>
</template>

<style scoped>
.swiper-pagination {
  position: relative;
  display: flex;
  justify-content: center;
  gap: 8px;
  margin-top: 32px;
}

.swiper-horizontal {
  width: 100%;
  height: 100%;
  min-height: 0;
}

img {
  height: 100%;
  object-fit: cover;
  border-radius: 14px;
  min-height: 0;
}

h4 {
  text-align: left;
  font-size: 30px;
  font-weight: 600;
  color: var(--ion-color-dark);
}

section {
  display: flex;
  flex-direction: column;
  gap: 16px;

  height: 100%;
  min-height: 0;
}
</style>
