<template>
  <ion-app>
    <PagesHeader />
    <ion-content>
      <ion-router-outlet id="main-content" />
    </ion-content>
  </ion-app>
</template>

<script setup lang="ts">
import { IonApp, IonRouterOutlet } from "@ionic/vue";
import { IonContent } from "@ionic/vue";
import PagesHeader from "@/components/PagesHeader.vue";

import "./theme/main.css";
</script>
