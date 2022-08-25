<template>
  <v-card>
    <v-card-text>
      <div class="elevation-1" id="qr-code-full-region"></div>
      <v-select
        class="mt-2"
        v-model="cameraId"
        label="Select Camera"
        outlined
        :items="cameraItems"
      ></v-select>
      <v-layout wrap v-if="devices.length > 0">
        <v-flex pa-1 md6 xl6 sm12 xs12>
          <v-btn block @click="startHandler">Start</v-btn>
        </v-flex>
        <v-flex pa-1 md6 xl6 sm12 xs12>
          <v-btn block @click="stopHandler">Stop</v-btn>
        </v-flex>
      </v-layout>
    </v-card-text>
  </v-card>
</template>

<script>
import { Html5Qrcode } from 'html5-qrcode'

export default {
  props: {
    qrbox: {
      type: Number,
      default: 250,
    },
    fps: {
      type: Number,
      default: 10,
    },
  },
  data() {
    return {
      devices: [],
      cameraId: null,
      html5QrCode: null,
    }
  },
  computed: {
    cameraItems() {
      return this.devices
    },
  },
  methods: {
    startHandler() {
      if (this.html5QrCode.getState() == 2) {
        this.stopHandler()
      }
      if (!this.cameraId) {
        return
      }
      this.html5QrCode
        .start(
          this.cameraId,
          {
            fps: this.fps, // Optional, frame per seconds for qr code scanning
            qrbox: { width: this.qrbox, height: this.qrbox }, // Optional, if you want bounded box UI
          },
          this.onDecode,
          this.onError
        )
        .catch((err) => {
          // Start failed, handle it.
          this.$emit('ErrorMessage', err)
        })
    },
    onError(errorMessage) {
      // parse error, ignore it.
      this.$emit('ErrorMessage', errorMessage)
    },
    onDecode(decodedText, decodedResult) {
      this.$emit('result', decodedText, decodedResult)
    },
    stopHandler() {
      if (this.html5QrCode.getState() == 2) {
        this.html5QrCode.stop().catch((err) => {
          this.$emit('ErrorMessage', err)
        })
      }
    },
  },
  mounted() {
    this.html5QrCode = new Html5Qrcode('qr-code-full-region')

    // This method will trigger user permissions
    Html5Qrcode.getCameras()
      .then((devices) => {
        devices.map((c) => this.devices.push({ text: c.label, value: c.id }))
      })
      .catch((err) => {
        console.log(err)
      })
  },
}
</script>
