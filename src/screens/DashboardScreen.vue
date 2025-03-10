<template>
  <div class="dashboard-screen p-4">
    <h2 class="text-xl font-bold mb-4">Tu Impacto Ambiental</h2>

    <!-- Gráficos circulares -->
    <div class="bg-white rounded-lg shadow-md p-4 mb-4">
      <h3 class="font-semibold mb-2">Progreso Mensual</h3>
      <div class="flex justify-center">
        <div class="relative w-40 h-40">
          <!-- Gráfico circular -->
          <svg class="w-full h-full" viewBox="0 0 100 100">
            <!-- Fondo del círculo -->
            <circle cx="50" cy="50" r="45" fill="none" stroke="#e6e6e6" stroke-width="10" />
            <!-- Progreso (75%) -->
            <circle cx="50" cy="50" r="45" fill="none" stroke="#3CB371" stroke-width="10" 
              stroke-dasharray="282.7" stroke-dashoffset="70.7" transform="rotate(-90 50 50)" />
            <text x="50" y="50" text-anchor="middle" dy="7" font-size="20" font-weight="bold" fill="#3CB371">75%</text>
            <text x="50" y="65" text-anchor="middle" dy="7" font-size="10" fill="#666">de la meta</text>
          </svg>
        </div>
      </div>
      <div class="text-center mt-2">
        <p class="text-sm text-gray-600">Has reciclado 15 de 20 envases este mes</p>
      </div>
    </div>

    <!-- Contador de CO2 -->
    <div class="bg-white rounded-lg shadow-md p-4 mb-4">
      <h3 class="font-semibold mb-2">CO₂ Ahorrado</h3>
      <div class="flex items-center justify-center">
        <LeafIcon class="h-8 w-8 text-green-500 mr-2" />
        <div class="text-2xl font-bold text-green-600">2.5 kg</div>
      </div>
      <div class="mt-2 bg-gray-200 rounded-full h-2.5">
        <div class="bg-green-500 h-2.5 rounded-full" style="width: 65%"></div>
      </div>
      <p class="text-xs text-center mt-1 text-gray-600">¡Estás a 1.5 kg de tu próxima insignia!</p>
    </div>

    <!-- Mapa de centros de reciclaje -->
    <div class="bg-white rounded-lg shadow-md p-4 mb-4">
      <h3 class="font-semibold mb-2">Centros de Reciclaje Cercanos</h3>
      <div class="relative h-48 bg-gray-100 rounded-lg overflow-hidden">
        <!-- Simulación de mapa -->
        <div class="absolute inset-0 bg-green-50">
          <div class="absolute top-1/4 left-1/3 bg-green-500 rounded-full h-4 w-4 border-2 border-white shadow-md pulse-animation"></div>
          <div class="absolute top-1/2 right-1/4 bg-green-500 rounded-full h-4 w-4 border-2 border-white shadow-md"></div>
          <div class="absolute bottom-1/3 left-1/2 bg-green-500 rounded-full h-4 w-4 border-2 border-white shadow-md"></div>
          <!-- Ubicación actual -->
          <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 bg-blue-500 rounded-full h-6 w-6 border-2 border-white shadow-md flex items-center justify-center">
            <div class="h-2 w-2 bg-white rounded-full"></div>
          </div>
        </div>
        <div class="absolute bottom-2 right-2">
          <button class="bg-white p-2 rounded-full shadow-md">
            <MapPinIcon class="h-5 w-5 text-gray-600" />
          </button>
        </div>
      </div>
      <div class="mt-2">
        <div class="text-sm font-medium">Centro más cercano: 1.2 km</div>
        <div class="text-xs text-gray-600">EcoPunto Central - Abierto hasta 20:00</div>
        <button @click="openDirections" class="mt-2 text-sm text-green-600 font-medium flex items-center">
          <NavigationIcon class="h-4 w-4 mr-1" />
          Cómo llegar
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { Leaf as LeafIcon, MapPin as MapPinIcon, Navigation as NavigationIcon } from 'lucide-vue-next';
import { defineEmits } from 'vue';

const emit = defineEmits(['changeScreen']);

const openDirections = () => {
  alert('Abriendo direcciones en la aplicación de mapas');
};
</script>

<style scoped>
/* Animación de pulso para el mapa */
.pulse-animation {
  position: relative;
}

.pulse-animation::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: rgba(60, 179, 113, 0.4);
  transform: translate(-50%, -50%);
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0% {
    transform: translate(-50%, -50%) scale(1);
    opacity: 1;
  }
  100% {
    transform: translate(-50%, -50%) scale(3);
    opacity: 0;
  }
}
</style>
