<template>
  <ion-card class="ion-padding">
    <ion-img :src="image" :alt="title" />
    <ion-card-header>
      <ion-card-title class="ion-text-center" color="danger">{{ title }}</ion-card-title>
    </ion-card-header>

    <ion-card-content>
      {{ description }}
    </ion-card-content>
  </ion-card>
</template>
  
<script>
import { IonCard, IonImg, IonCardContent, IonCardHeader, IonCardTitle } from '@ionic/vue';

export default {
  props: ['title', 'image', 'description'],

  components: { IonCard, IonImg, IonCardContent, IonCardHeader, IonCardTitle },
};
</script>