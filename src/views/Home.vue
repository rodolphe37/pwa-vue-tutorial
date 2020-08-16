<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>PWA Vérif Code postal</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ZipSearch v-on:get-zip="getZipInfo" />
      <ZipInfo v-bind:info="info" />
      <ClearInfo v-bind:info="info" v-on:clear-info="clearInfo" />
    </ion-content>
  </div>
</template>

<script>
import ZipSearch from "../components/ZipSearch";
import ZipInfo from "../components/ZipInfo";
import ClearInfo from "../components/ClearInfo";

export default {
  name: "Home",
  components: { ZipSearch, ZipInfo, ClearInfo },
  data() {
    return {
      info: null,
    };
  },
  methods: {
    async getZipInfo(zip) {
      const res = await fetch(`https://api.zippopotam.us/FR/${zip}`);
      if (res.status == 404) {
        this.showAlert();
      }
      this.info = await res.json();
    },
    clearInfo() {
      this.info = null;
    },
    showAlert() {
      return this.$ionic.alertController
        .create({
          header: "Non Valide !!!",
          message: "S'il vous plaît, entrez un code postal valide",
          buttons: ["ok"],
        })
        .then((a) => a.present());
    },
  },
};
</script>
