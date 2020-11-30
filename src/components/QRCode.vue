<template>
  <canvas ref="canvas"></canvas>
</template>

<script>
import QRCode from 'qrcode';

export default {
  name: "qr-code",
  props: {
    cords: String,
  },
  mounted() {
    this.generate();
  },
  watch: {
    cords() {
      this.generate();
    }
  },
  methods: {
    generate() {
      QRCode.toCanvas(this.$refs['canvas'], this.cords, {
        scale: 8
      })
    }
  }
}
</script>

<style scoped>
canvas {
  height: 35vh!important;
  width: 35vh!important;
}
</style>
