<script setup lang="ts">
import { IonButton, IonPage } from "@ionic/vue";
</script>

<template>
  <ion-page class="main">
    <section class="top-content">
      <img src="/image 8.png" alt="salle illusion" />
    </section>
    <section class="bottom-content">
      <h3>PARIS, FRANCE</h3>
      <h1>Bienvenue au Musée de l'illusion</h1>
      <h3>
        Venez découvrir les salles / installations que nous avons mis en place !
      </h3>
      <ion-button fill="outline" color="dark" routerLink="/rooms"
        >DÉCOUVRIR</ion-button
      >
    </section>
  </ion-page>
</template>

<style scoped>
.main {
  height: 100%;
  min-height: 0;
  padding: 32px;

  background-image: linear-gradient(
    -45deg,
    #7e33ac 0,
    var(--ion-color-light) 60%
  );
}

.top-content {
  height: calc(100% - 300px);
}

img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 14px;
}

.bottom-content {
  height: 300px;
}

h1 {
  font-size: 40px;
  font-weight: bold;
  line-height: 100%;

  color: #fff;
}

h3 {
  color: #b4b4b4;
  font-weight: bold;
}

@media (prefers-color-scheme: light) {
  .main {
    background-image: linear-gradient(-45deg, #983dd1 0, #ffffff 60%);
  }

  h1 {
    color: var(--ion-color-dark);
  }

  h3 {
    color: #474747;
  }
}
</style>
