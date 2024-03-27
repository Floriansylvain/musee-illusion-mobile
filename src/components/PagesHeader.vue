<script lang="ts" setup>
import {
  IonMenu,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButtons,
  IonMenuButton,
} from "@ionic/vue";
</script>

<template>
  <header>
    <h1>PARIS</h1>
    <ion-menu side="end" content-id="main-content" :swipe-gesture="false">
      <ion-header>
        <ion-toolbar>
          <ion-title>Menu Content</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content class="ion-padding">This is the menu content.</ion-content>
    </ion-menu>
    <ion-buttons slot="end" id="main-content">
      <ion-menu-button color="dark"></ion-menu-button>
    </ion-buttons>
  </header>
</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 32px 32px 16px 32px;
}

h1 {
  color: #b4b4b4;
  font-weight: bold;
  margin: 0;
  font-size: 20px;
}
</style>
