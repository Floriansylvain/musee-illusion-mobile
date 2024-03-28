<script lang="ts" setup>
import {
  IonMenu,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButtons,
  IonMenuButton,
  IonMenuToggle,
  IonItem,
  IonLabel,
} from "@ionic/vue";
</script>

<template>
  <header>
    <h1>PARIS</h1>
    <ion-menu side="end" content-id="main-content" :swipe-gesture="false">
      <ion-header>
        <ion-toolbar>
          <ion-title>Menu</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content class="ion-padding">
        <ion-menu-toggle>
          <router-link to="/setups">
            <ion-item>
              <ion-label>Installations</ion-label>
            </ion-item>
          </router-link>
          <router-link to="/rooms">
            <ion-item>
              <ion-label>Salles</ion-label>
            </ion-item>
          </router-link>
        </ion-menu-toggle>
      </ion-content>
    </ion-menu>
    <ion-buttons slot="end">
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
  background-color: var(--ion-color-light);
}

h1 {
  color: #b4b4b4;
  font-weight: bold;
  margin: 0;
  font-size: 20px;
}
</style>
