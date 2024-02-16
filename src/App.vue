<!-- QRCode.vue -->
<template>
  <div class="qr">
    <input v-model="inputText" type="text" placeholder="Enter text">
    <button @click="generateQRCode">Generate QR Code</button>
    <canvas ref="qrcodeCanvas"></canvas>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import QRCode from 'qrcode';

const qrcodeCanvas = ref(null)
const inputText = ref('')

const generateQRCode = () =>{
  const canvas = qrcodeCanvas.value;
  if (canvas && inputText.value.trim() !== ''){
    QRCode.toCanvas(canvas, inputText.value, { with: 200, height: 200 }, (error) =>{
      if(error){
        console.log(error)
      }
    })
  }
}

onMounted(() =>{
  generateQRCode()
})
</script>

<style scoped>
.qr{
  display: flex;
  flex-direction: column-reverse;
}
</style>
