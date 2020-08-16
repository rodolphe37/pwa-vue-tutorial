<template>
  <ion-grid>
    <form @submit="onSubmit">
      <ion-col>
        <ion-item>
          <ion-label>Code Postal:</ion-label>
          <ion-input
            :value="zip"
            @input="zip= $event.target.value"
            placeholder="Entrer le code postal"
            name="zip"
          ></ion-input>
        </ion-item>
      </ion-col>
      <ion-col>
        <ion-button type="submit" color="primary" expand="block">Chercher</ion-button>
      </ion-col>
    </form>
  </ion-grid>
</template>

<script>
export default {
  name: "ZipSearch",
  data() {
    return {
      zip: "",
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      // Zip Regex
      const isValidZip = /(^\d{5}$)|(^\d{5}-\d{4}$)/.test(this.zip);
      // Test for valid Zip
      if (!isValidZip) {
        this.showAlert();
        this.zip = "";
      } else {
        this.$emit("get-zip", this.zip);
        this.zip = "";
      }
    },
    showAlert() {
      return this.$ionic.alertController
        .create({
          header: "Entrez le code postal",
          message: "S'il vous plaît, entrez un code postal valide",
          buttons: ["ok"],
        })
        .then((a) => a.present());
    },
  },
};
</script>
