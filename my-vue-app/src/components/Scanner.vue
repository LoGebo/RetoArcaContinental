<template>
    <div class="scanner-component">
      <!-- Vista de cámara cuando está escaneando -->
      <div v-if="scanning" class="relative w-full max-w-sm aspect-[3/4] bg-black/5 rounded-lg overflow-hidden">
        <!-- Componente de escaneo de QR -->
        <qrcode-stream 
          @decode="onDecode" 
          @init="onInit"
          :camera="selectedCamera"
          :torch="torch"
          class="absolute inset-0"
        >
          <!-- Overlay de escaneo -->
          <div class="absolute inset-0 bg-gradient-to-b from-black/10 to-black/30">
            <!-- Área de escaneo con animación -->
            <div class="absolute inset-0 flex flex-col items-center justify-center">
              <div class="relative w-48 h-48 border-2 border-green-500 rounded-lg">
                <div class="absolute left-0 right-0 h-0.5 bg-green-500 animate-scan"></div>
              </div>
              <div class="mt-4 text-green-500 font-medium animate-pulse flex items-center gap-2">
                <QrCode class="w-5 h-5" />
                <span>Buscando código...</span>
              </div>
            </div>
          </div>
        </qrcode-stream>
        
        <!-- Botones de control -->
        <div class="absolute bottom-4 left-0 right-0 flex justify-center space-x-4">
          <button 
            v-if="hasTorch" 
            @click="toggleTorch" 
            class="bg-white/80 hover:bg-white p-2 rounded-full"
          >
            <Flashlight :class="torch ? 'text-yellow-500' : 'text-gray-700'" class="w-5 h-5" />
          </button>
          
          <button 
            v-if="cameras.length > 1" 
            @click="switchCamera" 
            class="bg-white/80 hover:bg-white p-2 rounded-full"
          >
          <span class="w-5 h-5 text-gray-700">🔄</span> 
          </button>
        </div>
        
        <!-- Botón para cerrar -->
        <button @click="stopScanning" class="absolute top-4 right-4 bg-white/80 hover:bg-white p-2 rounded-full">
          <X class="w-5 h-5" />
        </button>
      </div>
      
      <!-- Vista de inicio cuando no está escaneando -->
      <div v-else class="w-full max-w-sm bg-white shadow rounded-lg p-6">
        <div class="flex flex-col items-center gap-6">
          <div class="w-24 h-24 rounded-full bg-green-100 flex items-center justify-center">
            <QrCode class="w-10 h-10 text-green-500" />
          </div>
          
          <div class="text-center">
            <h2 class="text-lg font-medium mb-2">Escanea tu envase</h2>
            <p class="text-sm text-gray-600">
              Apunta la cámara al código de barras o QR del envase para verificar si es reciclable
            </p>
          </div>
          
          <button @click="startScanning" class="w-full bg-green-500 hover:bg-green-600 text-white py-2 px-4 rounded">
            Iniciar Escaneo
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import { QrcodeStream } from 'vue-qrcode-reader';
  import { QrCode, X, Flashlight } from 'lucide-vue-next';
  
  const emit = defineEmits(['scan-success', 'scan-error']);
  
  // Estado del escáner
  const scanning = ref(false);
  const cameras = ref([]);
  const selectedCamera = ref('auto');
  const hasTorch = ref(false);
  const torch = ref(false);
  const error = ref('');
  
  // Iniciar el escaneo
  const startScanning = () => {
    scanning.value = true;
  };
  
  // Detener el escaneo
  const stopScanning = () => {
    scanning.value = false;
  };
  
  // Manejar la inicialización de la cámara
  const onInit = async (promise) => {
    try {
      const { capabilities } = await promise;
      
      // Verificar si hay soporte para linterna
      hasTorch.value = capabilities.torch || false;
      
      // Obtener lista de cámaras disponibles
      if (navigator.mediaDevices && navigator.mediaDevices.enumerateDevices) {
        const devices = await navigator.mediaDevices.enumerateDevices();
        cameras.value = devices.filter(device => device.kind === 'videoinput');
      }
      
      error.value = '';
    } catch (err) {
      error.value = err.message || 'Error al inicializar la cámara';
      emit('scan-error', error.value);
      
      // Si hay un error de permisos, mostramos un mensaje específico
      if (err.name === 'NotAllowedError') {
        error.value = 'Necesitamos acceso a la cámara para escanear códigos QR';
      }
      
      // Si no hay cámara disponible
      if (err.name === 'NotFoundError') {
        error.value = 'No se encontró ninguna cámara en este dispositivo';
      }
      
      console.error('Error de inicialización de QR:', err);
      stopScanning();
    }
  };
  
  // Manejar la decodificación del QR
  const onDecode = (result) => {
    // Emitir el resultado del escaneo
    emit('scan-success', result);
    
    // Detener el escaneo después de un resultado exitoso
    stopScanning();
  };
  
  // Cambiar entre cámaras (frontal/trasera)
  const switchCamera = () => {
    if (cameras.value.length <= 1) return;
    
    // Si estamos usando la cámara frontal, cambiar a la trasera y viceversa
    const currentIndex = cameras.value.findIndex(camera => camera.deviceId === selectedCamera.value);
    const nextIndex = (currentIndex + 1) % cameras.value.length;
    selectedCamera.value = cameras.value[nextIndex].deviceId;
  };
  
  // Activar/desactivar la linterna
  const toggleTorch = () => {
    if (!hasTorch.value) return;
    torch.value = !torch.value;
  };
  </script>
  
  <style scoped>
  .animate-scan {
    animation: scanMove 2s ease-in-out infinite;
  }
  
  @keyframes scanMove {
    0%, 100% { top: 20px; }
    50% { top: calc(100% - 20px); }
  }
  </style>