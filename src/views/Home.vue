<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>PWA Vérif Code postal</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ZipSearch v-on:get-zip="getZipInfo" />
    </ion-content>
  </div>
</template>

<script>
import ZipSearch from "../components/ZipSearch";
export default {
  name: "Home",
  components: { ZipSearch },
  methods: {
    async getZipInfo(zip) {
      const res = await fetch(`https://api.zippopotam.us/FR/${zip}`);
      if (res.status == 404) {
        this.showAlert();
      }
      const info = await res.json();

      console.log(info);
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
