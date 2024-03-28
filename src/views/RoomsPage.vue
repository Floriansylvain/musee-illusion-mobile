<script setup lang="ts">
import { IonPage } from "@ionic/vue";
import { onMounted, ref } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import { CapacitorHttp } from "@capacitor/core";

import IllusionSwiper from "@/components/IllusionSwiper.vue";

import "swiper/css";
import "swiper/css/pagination";

const data = ref();
const currentRoomIndex = ref(0);

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
    <swiper direction="vertical" class="swiper-vertical">
      <swiper-slide class="top-content">
        <main>
          <h2>Les salles</h2>
          <h3>Venez découvrir les salles mises en place !</h3>

          <IllusionSwiper
            :data="data"
            @on-slide-index-change="(i) => (currentRoomIndex = i)"
          />
        </main>
      </swiper-slide>
      <swiper-slide class="bottom-content">
        <h2>{{ data && data[currentRoomIndex].fields.titre }}</h2>
        <p>{{ data && data[currentRoomIndex].fields.description }}</p>
      </swiper-slide>
    </swiper>
  </ion-page>
</template>

<style scoped>
.page {
  background-color: var(--ion-color-light);

  justify-content: start;
  height: 100%;
  min-height: 0;
}

section {
  display: flex;
  flex-direction: column;
  gap: 16px;

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

.swiper-vertical {
  width: 100%;
  height: 100%;
  min-height: 0;
}

audio {
  width: 100%;
}

.top-content {
  display: flex;
  flex-direction: column;
  height: 100%;
  min-height: 0;
}

.bottom-content {
  display: flex;
  flex-direction: column;
  gap: 16px;

  padding: 32px;

  height: 100%;
  min-height: 0;

  background-image: linear-gradient(
    -45deg,
    #7e33ac 0,
    var(--ion-color-light) 60%
  );
}

.bottom-content h2 {
  font-size: 50px;
  font-weight: bold;
  margin: 0;
}

.bottom-content p {
  font-size: 27px;
  font-weight: 500;
  color: var(--ion-color-dark);
  margin: 0;
}
</style>
