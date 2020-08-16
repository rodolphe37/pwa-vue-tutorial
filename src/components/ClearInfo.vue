<template>
  <ion-button color="light" expand="block" v-if="info" @click="$emit('clear-info')">Effacer</ion-button>
</template>

<script>
export default {
  name: "ClearInfo",
  props: ["info"],
};
</script>
