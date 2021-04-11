<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Devices</ion-title>
        <ion-buttons slot="end">
          <ion-button @click="addDevice('my dev', 'http://192.168.0.1:8080')">
            <ion-icon name="add"></ion-icon>
          </ion-button>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Devices</ion-title>
        </ion-toolbar>
      </ion-header>

      <ion-list ref="list">
        <ion-item-sliding v-for="(device, index) in devices" :key="index">
          <ion-item>
            <ion-label>{{ device.name }}</ion-label>
            <ion-label>{{ device.host }}</ion-label>
          </ion-item>
          <ion-item-options slot="end">
            <ion-item-option>Edit</ion-item-option>
            <ion-item-option color="danger" @click="deleteDevice(index)">Delete</ion-item-option>
          </ion-item-options>
        </ion-item-sliding>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButtons, IonButton, IonIcon, IonItem, IonList, IonItemSliding, IonItemOption, IonItemOptions, IonLabel } from '@ionic/vue';
import { add } from "ionicons/icons";
import { addIcons } from "ionicons";
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Home',
  components: { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButtons, IonButton, IonIcon, IonItem, IonList, IonItemSliding, IonItemOptions, IonItemOption, IonLabel },
  data() {
    return {
      devices: [],
      i: 0
    };
  },
  methods: {
    addDevice: function(name, host) {
      this.devices.push({name: this.i.toString(), host});
      this.i++;
    },
    deleteDevice: function(index) {
      this.$refs.list.$el.closeSlidingItems();
      this.devices.splice(index, 1);
    }
  },
  mounted() {
    addIcons({
      add: add
    });
  }
});
</script>

<style scoped>
</style>