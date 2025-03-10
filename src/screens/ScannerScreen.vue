<template>
  <div class="scanner-screen">
    <div class="relative h-[70vh] bg-black flex items-center justify-center">
      <div id="reader" class="w-full h-full"></div>
    </div>

    <!-- Instructions -->
    <div class="absolute bottom-0 left-0 right-0 bg-black bg-opacity-70 text-white p-4">
      <p class="text-center">Escanea el código QR</p>
    </div>

    <!-- Notification Popup -->
    <div v-if="showNotification" class="fixed inset-x-0 top-20 mx-auto w-5/6 bg-white rounded-lg shadow-lg p-4 z-50">
      <div class="flex items-start">
        <div class="bg-green-100 rounded-full p-2 mr-3">
          <CheckCircleIcon class="h-6 w-6 text-green-600" />
        </div>
        <div class="flex-1">
          <h3 class="font-bold">¡Código QR detectado!</h3>
          <p class="text-sm text-gray-600">Código: {{ scannedCode }}</p>
        </div>
        <button @click="showNotification = false" class="text-gray-400 hover:text-gray-600">
          <XIcon class="h-5 w-5" />
        </button>
      </div>
      <div class="mt-3">
        <button @click="processContainer" class="w-full bg-green-500 hover:bg-green-600 text-white py-2 rounded-lg">
          Procesar código
        </button>
      </div>
    </div>

    <!-- Floating Button to Activate Scanner -->
    <button @click="toggleScanner" class="fixed bottom-24 right-6 bg-green-500 hover:bg-green-600 text-white rounded-full p-4 shadow-lg">
      <CameraIcon class="h-6 w-6" />
    </button>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";
import { Html5QrcodeScanner } from "html5-qrcode";

const scannerActive = ref(false);
const showNotification = ref(false);
const scannedCode = ref("");
let html5QrcodeScanner;

const toggleScanner = () => {
  scannerActive.value = !scannerActive.value;
  if (scannerActive.value) {
    startScanner();
  } else {
    stopScanner();
  }
};

const startScanner = () => {
  html5QrcodeScanner = new Html5QrcodeScanner(
    "reader",
    { fps: 10, qrbox: 250 },
    false
  );
  html5QrcodeScanner.render(onScanSuccess, onScanError);
};

const stopScanner = () => {
  if (html5QrcodeScanner) {
    html5QrcodeScanner.clear();
  }
};

const onScanSuccess = (decodedText) => {
  scannedCode.value = decodedText;
  showNotification.value = true;
  scannerActive.value = false; // Stop scanner after detection
  stopScanner();

  // Redirect to the scanned URL
  window.location.href = decodedText;
};

const onScanError = (error) => {
  console.error("Scan error:", error);
};

const processContainer = () => {
  showNotification.value = false;
};

onMounted(() => {
  if (scannerActive.value) {
    startScanner();
  }
});

onBeforeUnmount(() => {
  stopScanner();
});
</script>

<style>
.scan-line {
  position: absolute;
  height: 2px;
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