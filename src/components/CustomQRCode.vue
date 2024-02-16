<template>
  <div>
    <input v-model="text" placeholder="Enter text for QR code">
    <canvas ref="canvas" :width="size" :height="size"></canvas>
  </div>
</template>

<script>
import QRCode from 'qrcode';

export default {
  name: 'CustomQRCode',
  data() {
    return {
      text: '',
      size: 300,
    };
  },
  watch: {
    text: function() {
      this.generateQRCode();
    },
  },
  mounted() {
    this.generateQRCode();
  },
  methods: {
    async generateQRCode() {
      const canvas = this.$refs.canvas;
      const context = canvas.getContext('2d');

      // Clear canvas
      context.clearRect(0, 0, this.size, this.size);

      // Generate QR code
      const qrCodeText = this.text;
      const qrCodeOptions = {
        errorCorrectionLevel: 'H',
        type: 'image/jpeg',
        rendererOpts: {
          quality: 0.3,
        },
      };

      const qrCode = await QRCode.toCanvas(canvas, qrCodeText, qrCodeOptions);

      // Add image to QR code
      const image = new Image();
      image.src = '../../public/vite.svg'; // Замініть це на шлях до вашого зображення
      image.onload = () => {
        context.drawImage(image, 100, 100, 100, 100); // Розміщення та розміри вашого зображення
      };
    },
  },
};
</script>
