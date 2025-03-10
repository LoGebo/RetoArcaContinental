
<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

// Estado de la aplicación
const currentScreen = ref('scanner');
const showNotification = ref(false);
const showShareModal = ref(false);

// Timer para la promoción
const timer = ref({
  hours: '05',
  minutes: '23',
  seconds: '47'
});

// Iniciar el temporizador
let timerInterval;
onMounted(() => {
  // Actualizar el temporizador cada segundo
  timerInterval = setInterval(() => {
    let h = parseInt(timer.value.hours);
    let m = parseInt(timer.value.minutes);
    let s = parseInt(timer.value.seconds);
    
    s--;
    if (s < 0) {
      s = 59;
      m--;
      if (m < 0) {
        m = 59;
        h--;
        if (h < 0) {
          h = 0;
          m = 0;
          s = 0;
          clearInterval(timerInterval);
        }
      }
    }
    
    timer.value.hours = h.toString().padStart(2, '0');
    timer.value.minutes = m.toString().padStart(2, '0');
    timer.value.seconds = s.toString().padStart(2, '0');
  }, 1000);
});

onUnmounted(() => {
  clearInterval(timerInterval);
});

// Funciones
const activateScanner = () => {
  // Simular detección de código después de 2 segundos
  setTimeout(() => {
    showNotification.value = true;
  }, 2000);
};

const processContainer = () => {
  showNotification.value = false;
  currentScreen.value = 'traceability';
};


const viewOnMap = () => {
  currentScreen.value = 'dashboard';
};

const viewReward = () => {
  currentScreen.value = 'rewards';
  setTimeout(() => {
    showConfetti.value = true;
  }, 500);
};

const openDirections = () => {
  // En una app real, esto abriría la aplicación de mapas
  alert('Abriendo direcciones en la aplicación de mapas');
};

import Navbar from './components/Navbar.vue';
import BottomNavigation from './components/BottomNavigation.vue';
import ScannerScreen from './screens/ScannerScreen.vue';
import DashboardView from './screens/DashboardScreen.vue';
import HomeView from './screens/HomeScreen.vue';
import TraceabilityView from './screens/TraceabilityScreen.vue';
import NotificationsView from './screens/NotificationsScreen.vue';
import RewardsView from './screens/RewardsScreen.vue';
import ProfileScreen from './screens/ProfileScreen.vue';

</script>


<template>
  <div class="font-sans text-gray-800 bg-gray-50 min-h-screen max-w-md mx-auto relative overflow-hidden">
  
  
    <!-- Barra de navegación SUPERIOR SUPERIOR -->
    <Navbar @changeScreen="currentScreen = $event" />

    <!-- Contenido principal -->
    <main class="pb-20">

      <ScannerScreen v-if="currentScreen === 'scanner'" @changeScreen="currentScreen = $event" />

      <DashboardView v-if="currentScreen === 'dashboard'" @changeScreen="currentScreen = $event" />

      <HomeView v-if="currentScreen === 'home'" @openRewardModal="showRewardModal = true" />

      <TraceabilityView v-if="currentScreen === 'traceability'" />

      <RewardsView v-if="currentScreen === 'rewards'" />

      <!-- Esta se renderiza a partir de la barra de navegacion d arriba -->
      <NotificationsView v-if="currentScreen === 'notifications'" />

      <ProfileScreen v-if="currentScreen === 'profile'" />

      
    </main>

    <!-- TAB BAR TAB BAR TAB BAR TAB BAR TAB BAR -->
    <BottomNavigation @changeScreen="currentScreen = $event" />
    
  </div>
</template>



<style>
/* Animación del escáner */
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
  0% {
    top: 0;
  }
  50% {
    top: 100%;
  }
  100% {
    top: 0;
  }
}

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

/* Animación de confeti */
.confetti-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 100;
  overflow: hidden;
}

.confetti {
  position: absolute;
  width: 10px;
  height: 10px;
  background: var(--confetti-color);
  top: -10px;
  left: var(--left-pos);
  opacity: 0;
  transform: rotate(0);
  animation: fall var(--fall-duration) var(--fall-delay) linear forwards;
}

@keyframes fall {
  0% {
    top: -10px;
    transform: rotate(0);
    opacity: 0;
  }
  25% {
    opacity: 1;
  }
  100% {
    top: 100vh;
    transform: rotate(360deg);
    opacity: 0;
  }
}
</style>