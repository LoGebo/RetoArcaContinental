<template>
  <div class="traceability-screen p-4">
    <h2 class="text-xl font-bold mb-4">Trazabilidad del Envase</h2>

    <div class="bg-white rounded-lg shadow-md p-4 mb-4">
      <div class="flex items-center mb-3">
        <div class="bg-green-100 p-2 rounded-full mr-3">
          <PackageIcon class="h-6 w-6 text-green-600" />
        </div>
        <div>
          <h3 class="font-semibold">{{ packageInfo.name }}</h3>
          <p class="text-xs text-gray-600">ID: {{ packageInfo.id }}</p>
        </div>
        <div class="ml-auto flex items-center">
          <LockIcon class="h-4 w-4 text-green-600 mr-1" />
          <span class="text-xs text-green-600">Verificado</span>
        </div>
      </div>

      <!-- Timeline dinámico -->
      <div class="relative pl-8 border-l-2 border-green-200 space-y-6 py-2">
        <div v-for="(event, index) in traceabilityEvents" :key="index" class="relative">
          <div class="absolute -left-10 mt-1.5 h-5 w-5 rounded-full border-4 border-green-500 bg-white"></div>
          <div class="flex flex-col">
            <h4 class="font-medium">{{ event.title }}</h4>
            <span class="text-xs text-gray-600">{{ event.date }}</span>
            <p class="text-sm mt-1">{{ event.description }}</p>
            <div class="flex items-center mt-1 text-xs text-green-600">
              <LinkIcon class="h-3 w-3 mr-1" />
              <span>Verificado en blockchain</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="bg-green-50 rounded-lg p-4 border border-green-200">
      <div class="flex items-start">
        <div class="bg-green-100 rounded-full p-1.5 mr-3">
          <InfoIcon class="h-5 w-5 text-green-600" />
        </div>
        <div>
          <h4 class="font-medium">Impacto de este envase</h4>
          <p class="text-sm mt-1">
            Este envase será transformado en nuevos productos, ahorrando {{ packageInfo.co2Saved }} kg de CO₂
            y {{ packageInfo.waterSaved }} litros de agua.
          </p>
        </div>
      </div>
      <button @click="openShareModal" class="mt-3 w-full flex items-center justify-center bg-green-500 hover:bg-green-600 text-white py-2 rounded-lg transition-colors">
        <ShareIcon class="h-4 w-4 mr-2" />
        Compartir mi impacto
      </button>
    </div>

    <!-- Modal de compartir impacto -->
    <ModalShare :isOpen="showShareModal" @close="closeShareModal" />

  </div>
</template>

<script setup>
import { ref } from 'vue';
import { Package as PackageIcon, Lock as LockIcon, Info as InfoIcon, Share as ShareIcon, Link as LinkIcon } from 'lucide-vue-next';
import ModalShare from '../modals/ModalShare.vue';

// Estado del modal de compartir
const showShareModal = ref(false);

// Función para abrir el modal de compartir impacto
const openShareModal = () => {
  showShareModal.value = true;
};

// Función para cerrar el modal de compartir impacto
const closeShareModal = () => {
  showShareModal.value = false;
};

// Simulación de datos del envase
const packageInfo = ref({
  name: "Botella PET - 500ml",
  id: "#BT28937465",
  co2Saved: "0.15",
  waterSaved: "2"
});

// Simulación de eventos de trazabilidad
const traceabilityEvents = ref([
  {
    title: "Producción",
    date: "15 Feb 2025 - 10:30",
    description: "Fabricado en Planta EcoPlásticos"
  },
  {
    title: "Distribución",
    date: "18 Feb 2025 - 08:45",
    description: "Centro Logístico Norte → Supermercado Eco"
  },
  {
    title: "Venta",
    date: "25 Feb 2025 - 16:20",
    description: "Adquirido en Supermercado Eco"
  },
  {
    title: "Reciclaje",
    date: "28 Feb 2025 - 14:05",
    description: "Depositado en EcoPunto Central"
  }
]);

// Función para compartir impacto
const shareImpact = () => {
  alert("Impacto compartido en redes sociales.");
};
</script>

<style scoped>
/* Animación del timeline */
.timeline-dot {
  position: absolute;
  left: -12px;
  top: 0;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: green;
}
</style>
