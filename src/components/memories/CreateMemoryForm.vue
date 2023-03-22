<template>
    <form class="ion-padding" @submit.prevent="submitForm">
        <ion-list>
            <ion-item>
                <ion-label position="floating">Title</ion-label>
                <ion-input type="text" required v-model="enteredTitle" />
            </ion-item>
            <ion-item>
                <ion-thumbnail slot="start">
                    <ion-img :src="imagePreviewUrl" />
                </ion-thumbnail>
                <ion-button fill="clear" type="button" @click="takePhoto">
                    <ion-icon slot="start" :icon="camera"></ion-icon>
                    Take Photo
                </ion-button>
            </ion-item>
            <ion-item>
                <ion-label position="floating">Description</ion-label>
                <ion-textarea rows="6" v-model="enteredDescription"></ion-textarea>
            </ion-item>
        </ion-list>
        <ion-button type="submit" color="danger" shape="round" expand="block" class="ion-margin-top"
            fill="outline">Save</ion-button>
    </form>
</template>

<script>
import {
    IonList,
    IonItem,
    IonLabel,
    IonInput,
    IonTextarea,
    IonButton,
    IonThumbnail,
    IonImg,
    IonIcon
} from "@ionic/vue";
import { camera } from 'ionicons/icons';
import { Camera, CameraResultType, CameraSource } from '@capacitor/camera';

/* const { Camera } = Plugins; */

export default {
    emits: ["save-memory"],

    components: {
        IonList,
        IonItem,
        IonLabel,
        IonInput,
        IonTextarea,
        IonButton,
        IonThumbnail,
        IonImg,
        IonIcon
    },

    data() {
        return {
            enteredTitle: "",
            enteredDescription: "",
            /* takenImageUrl: null, */
            imagePreviewUrl: null,
            camera
        };
    },

    methods: {
        submitForm() {
            const memoryData = {
                title: this.enteredTitle,
                imageUrl: this.imagePreviewUrl,
                description: this.enteredDescription,
            };
            this.$emit("save-memory", memoryData);
        },
        async takePhoto() {
            const photo = await Camera.getPhoto({
                resultType: CameraResultType.Uri,
                source: CameraSource.Camera,
                quality: 70,
            });
            this.imagePreviewUrl = photo.webPath;
        },
    },
};
</script>