<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Devices</ion-title>
        <ion-buttons slot="end">
          <ion-button @click="openAddDevicePopup()">
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

      <div v-if="devices.length === 0" class="container">
        <p>It seems like you have not added any device yet.</p>
        <p>Tap the "+" icon to continue.</p>
      </div>
      <ion-list v-else>
        <Device
            v-for="(device, index) in devices"
            :key="index"
            @edit="editDevice(index)"
            @delete="deleteDevice(index)"
            :device="device"
        ></Device>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script>
import {
  IonButton,
  IonButtons,
  IonContent,
  IonHeader,
  IonIcon,
  IonList,
  IonPage,
  IonTitle,
  IonToolbar
} from '@ionic/vue';
import {add} from "ionicons/icons";
import {addIcons} from "ionicons";
import Device from "@/components/Device";

export default {
  name: 'Devices',
  components: { Device, IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButtons, IonButton, IonIcon, IonList },
  data() {
    return {
      devices: this.getDevices()
    };
  },
  computed: {
  },
  methods: {
    addDevice(name, url) {
      this.devices.push({name: name, url: url});
      this.saveDevices(this.devices);
    },
    deleteDevice(index) {
      this.devices.splice(index, 1);
      this.saveDevices(this.devices);
    },
    editDevice(index) {
      // TODO
      console.log("TODO: edit device" + index);
    },
    saveDevices(devices){
      localStorage.setItem("devices", JSON.stringify(devices));
    },
    getDevices(){
      const devices = localStorage.getItem("devices");
      return devices ? JSON.parse(devices) : [];
    },
    openAddDevicePopup() {
      // TODO
      this.addDevice('My LedWall (Basement Party Room)', 'http://localhost:8080');
    }
  },
  mounted() {
    addIcons({
      add: add
    });
  }
}
</script>

<style scoped>
.container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}
</style>
