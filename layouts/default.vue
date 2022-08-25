<template>

  <v-app>
      <v-main>
        <v-container><Nuxt /></v-container>
      </v-main>
    </v-app>
</template>
<script>
export default {

   head() {
    return {
    title: 'Nuxt play ground 🤪',

    }
  },
  methods:{
     downloadPdf() {
      this.$refs.html2Pdf.generatePdf();
    },
  }
}
</script>
