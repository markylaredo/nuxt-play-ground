<template>
  <v-card>
    <v-btn @click="cmpVModel">Component v-model</v-btn>
    <v-btn @click="dynamicFields">Table dynamic fields</v-btn>
    <v-btn @click="qrCodeScanner">QrCode/Barcode Scanner</v-btn>
    <v-btn to="/table/custom-data-table">Custom Data Table</v-btn>
    <v-card-text> </v-card-text>
    <div class="container">
      <nuxt-child />
    </div>
  </v-card>
</template>

<script>
export default {
  methods: {
    cmpVModel() {
      this.$router.push('/v-model-in-component')
    },
    dynamicFields() {
      this.$router.push('/table/fields')
    },
    qrCodeScanner() {
      this.$router.push('/qr-code-scanner')
    },
  },
}
</script>
