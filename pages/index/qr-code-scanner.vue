<script>
export default {
  data() {
    return {
      decodedText: null,
      decodedResult: null,
    }
  },
  methods: {
    onDecode(decodedText, decodedResult) {
      this.decodedText = decodedText
      this.decodedResult = decodedResult
    },
  },
}
</script>
<template>
  <div>
    QR Code and Barcode scanner using this package
    <pre>https://github.com/mebjas/html5-qrcode</pre>
    <br />
    <br />
    DEMO:
    <qrcode-scanner
      :qrbox="240"
      :fps="20"
      style="width: 500px"
      @result="onDecode"
    />
    <pre>decodedText: {{ decodedText }}</pre>
    <pre>decodedResult: {{ decodedResult }}</pre>
  </div>
</template>
