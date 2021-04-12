<template>
  <ion-item-sliding ref="item">
    <ion-item>
      <div>
        <ion-label>{{ device.name }}</ion-label>
        <ion-label>{{ device.url }}</ion-label>
        <ion-label v-if="deviceType">Online - {{ deviceType }}</ion-label>
        <ion-label v-else>Offline</ion-label>
      </div>
    </ion-item>
    <ion-item-options slot="end">
      <ion-item-option @click="edit()">Edit</ion-item-option>
      <ion-item-option @click="remove()" color="danger">Delete</ion-item-option>
    </ion-item-options>
  </ion-item-sliding>
</template>

<script>
import { IonItemSliding, IonItem, IonLabel, IonItemOptions, IonItemOption } from "@ionic/vue";

export default {
  name: 'Device',
  props: ["device"],
  components: { IonItemSliding, IonItem, IonLabel, IonItemOptions, IonItemOption },
  data() {
    return {
      deviceType: undefined
    }
  },
  methods: {
    edit() {
      this.close();
      setTimeout(() => {
        this.$emit("edit");
      }, 300);
    },
    remove() {
      this.close();
      setTimeout(() => {
        this.$emit("delete");
      }, 300);
    },
    close(){
      this.$refs.item.$el.close();
    }
  },
  mounted() {
    fetch(this.device.url)
      .then((response) => response.json())
      .then((json) => this.deviceType = json.deviceType)
      .catch(() => this.deviceType = undefined);
  }
}
</script>
