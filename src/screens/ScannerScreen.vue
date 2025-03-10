<template>
  <div class="scanner-screen">
    <div class="relative h-screen bg-black flex flex-col justify-center items-center">
      
      <!-- UI Scanner Frame -->
      <div class="relative w-3/4 h-3/4 flex items-center justify-center">
        <div class="qr-frame border-2 border-green-500 w-80 h-80 relative">
          <div class="absolute top-0 left-0 w-10 h-10 border-t-4 border-l-4 border-green-500"></div>
          <QrcodeStream @decode="onScanSuccess" @init="onScanInit" @error="onScanError" />
          <div class="absolute top-0 right-0 w-10 h-10 border-t-4 border-r-4 border-green-500"></div>
          <div class="absolute bottom-0 left-0 w-10 h-10 border-b-4 border-l-4 border-green-500"></div>
          <div class="absolute bottom-0 right-0 w-10 h-10 border-b-4 border-r-4 border-green-500"></div>
          <div class="scan-line"></div>
        </div>
      </div>

      <!-- Instructions -->
      <div class="absolute top-6 left-0 right-0 bg-black bg-opacity-70 text-white p-4 text-center">
        <p>Escanea el código de barras del envase</p>
      </div>
    </div>

    <!-- Notification Popup -->
    <div v-if="showNotification" class="fixed inset-x-0 top-20 mx-auto w-5/6 bg-white rounded-lg shadow-lg p-4 z-50">
      <div class="flex items-start">
        <div class="bg-green-100 rounded-full p-2 mr-3">
          <CheckCircleIcon class="h-6 w-6 text-green-600" />
        </div>
        <div class="flex-1">
          <h3 class="font-bold">¡Envase válido detectado!</h3>
          <p class="text-sm text-gray-600">Código: {{ scannedCode }}</p>
        </div>
        <button @click="showNotification = false" class="text-gray-400 hover:text-gray-600">
          <XIcon class="h-5 w-5" />
        </button>
      </div>
      <div class="mt-3">
        <button @click="processContainer" class="w-full bg-green-500 hover:bg-green-600 text-white py-2 rounded-lg">
          Procesar envase
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { QrcodeStream } from "vue-qrcode-reader";

const showNotification = ref(false);
const scannedCode = ref("");

const onScanSuccess = (code) => {
  scannedCode.value = code;
  showNotification.value = true;
  
  // Redirect to a URL or handle scan result
  window.location.href = `https://www.google.com/search?q=${code}`;
};

const onScanError = (error) => {
  console.error("Scan error:", error);
};

const processContainer = () => {
  showNotification.value = false;
};
</script>

<style>
.scan-line {
  position: absolute;
  height: 3px;
  width: 100%;
  background: #3CB371;
  top: 0;
  box-shadow: 0 0 8px 2px rgba(60, 179, 113, 0.8);
  animation: scan 2s linear infinite;
}

@keyframes scan {
  0% { top: 0; }
  50% { top: 100%; }
  100% { top: 0; }
}
</style>
