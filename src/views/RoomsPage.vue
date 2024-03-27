<script setup lang="ts">
import { IonPage } from "@ionic/vue";
import PagesHeader from "@/components/PagesHeader.vue";
import { onMounted, ref } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Pagination } from "swiper/modules";
import { CapacitorHttp } from "@capacitor/core";

import "swiper/css";
import "swiper/css/pagination";

const data = ref();

const getRooms = async () => {
  const options = {
    url: "https://api.airtable.com/v0/appjEyYgBdj0qnspK/salles?maxRecords=3&view=Grid%20view",
    headers: {
      Authorization:
        "Bearer patiOFBtQASKft57I.34999adcb6a30891dfeb090e2ee4f0cd82a0177f63041468474aa8243a9dc284",
    },
  };
  return await CapacitorHttp.get(options);
};

onMounted(async () => {
  const response = await getRooms();
  data.value = response.data?.records;
});
</script>

<template>
  <ion-page class="page">
    <PagesHeader />
    <main>
      <h2>Les salles</h2>
      <h3>Venez découvrir les salles mises en place !</h3>

      <swiper
        :pagination="{
          clickable: true,
          el: '.swiper-pagination',
          bulletClass: 'pagination-bullet',
          bulletActiveClass: 'pagination-bullet-active',
        }"
        :modules="[Pagination]"
        :space-between="250"
        :auto-height="false"
        class="mySwiper"
      >
        <swiper-slide v-for="element in data" :key="element.titre">
          <section>
            <h4>{{ element.fields.titre }}</h4>
            <img :src="element.fields.image[0].url" alt="hallan" />
            <audio controls :src="element.fields.audio[0].url"></audio>
          </section>
        </swiper-slide>
      </swiper>
      <div slot="pagination" class="swiper-pagination"></div>
    </main>
  </ion-page>
</template>

<style scoped>
.page {
  background-color: var(--ion-color-light);

  justify-content: start;
  height: 100vh;
}

section {
  display: flex;
  flex-direction: column;
  gap: 8px;

  height: 100%;
  min-height: 0;
}

main {
  display: flex;
  flex-direction: column;

  padding: 0 32px 32px 32px;

  height: 100%;
  min-height: 0;
}

h2 {
  font-size: 60px;
  font-weight: bold;
  color: var(--ion-color-dark);
  margin: 0;
}

h3 {
  font-size: 27px;
  font-weight: 600;
  color: #b4b4b4;
  margin: 0;
}

h4 {
  text-align: left;
  font-size: 30px;
  font-weight: 600;
  color: var(--ion-color-dark);
}

img {
  width: 100%;
  object-fit: cover;
  border-radius: 14px;
  min-height: 0;
}

audio {
  width: 100%;
}

.swiper-pagination {
  position: relative;
  display: flex;
  justify-content: center;
  gap: 8px;
  margin-top: 16px;
}

.mySwiper {
  width: 100%;
  height: 100%;
  min-height: 0;
}
</style>

<style>
.pagination-bullet,
.pagination-bullet-active {
  width: 48px;
  height: 4px;
  background-color: var(--ion-color-medium);
  border-radius: 8px;
}

.pagination-bullet-active {
  background-color: var(--ion-color-dark);
}
</style>
