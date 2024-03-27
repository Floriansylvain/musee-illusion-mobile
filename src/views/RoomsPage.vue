<script setup lang="ts">
import { IonPage, IonContent } from "@ionic/vue";
import PagesHeader from "@/components/PagesHeader.vue";
import { onMounted, ref } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Pagination } from "swiper/modules";
import { CapacitorHttp } from "@capacitor/core";

import "swiper/css";
import "swiper/css/pagination";

const data = ref();

const doGet = async () => {
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
  const response = await doGet();
  data.value = response.data?.records;
  console.table(data.value[0].fields.audio);
});
</script>

<template>
  <ion-page class="page">
    <ion-content color="light">
      <PagesHeader />
      <main>
        <h2>Les salles</h2>
        <h3>Venez découvrir les salles mises en place !</h3>

        <swiper
          :pagination="{
            clickable: true,
            el: '.swiper-pagination',
            bulletClass: 'swiper-pagination-bullet-custom',
            bulletActiveClass: 'swiper-pagination-bullet-active-custom',
          }"
          :modules="[Pagination]"
          :space-between="50"
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
    </ion-content>
  </ion-page>
</template>

<style scoped>
.page {
  background-color: var(--ion-color-light);

  justify-content: start;
}

ion-content {
  display: flex;
  flex-direction: column;
  gap: 8px;

  height: 100%;
}

main {
  padding: 0 32px 32px 32px;
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

.swiper-pagination-bullet-custom {
  width: 20px;
  height: 20px;
  border-radius: 50%;
}

.swiper-pagination-bullet-active-custom {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: red !important;
}
</style>
