<template>
    <div class="rewards-screen p-4">
      <h2 class="text-xl font-bold mb-4">Sistema de Recompensas</h2>
  
      <!-- Barra de progreso de nivel -->
      <div class="bg-white rounded-lg shadow-md p-4 mb-4">
        <div class="flex justify-between items-center mb-2">
          <span class="font-semibold">Nivel 3</span>
          <span class="text-sm text-gray-600">450 / 500 puntos</span>
        </div>
        <div class="h-4 bg-gray-200 rounded-full overflow-hidden">
          <div class="h-full bg-gradient-to-r from-green-400 to-green-600" style="width: 90%"></div>
        </div>
        <div class="flex justify-between text-xs mt-1">
          <span>Nivel actual</span>
          <span>Nivel 4</span>
        </div>
      </div>
  
      <!-- Catálogo de premios -->
      <h3 class="font-semibold mb-2">Premios Disponibles</h3>
      <div class="space-y-3">
        <div class="bg-white rounded-lg shadow-md p-3 border-l-4 border-green-500">
          <div class="flex justify-between items-center">
            <div>
              <h4 class="font-medium">Descuento 15% Tienda Eco</h4>
              <p class="text-xs text-gray-600">Válido en productos sostenibles</p>
            </div>
            <div class="bg-green-100 text-green-800 text-xs font-semibold px-2 py-1 rounded">
              200 pts
            </div>
          </div>
          <button @click="redeemReward(1)" class="mt-2 w-full bg-green-500 hover:bg-green-600 text-white py-1.5 rounded text-sm transition-colors">
            Canjear
          </button>
        </div>
  
        <div class="bg-white rounded-lg shadow-md p-3 border-l-4 border-blue-500">
          <div class="flex justify-between items-center">
            <div>
              <h4 class="font-medium">Donación a Reforestación</h4>
              <p class="text-xs text-gray-600">Plantamos un árbol en tu nombre</p>
            </div>
            <div class="bg-blue-100 text-blue-800 text-xs font-semibold px-2 py-1 rounded">
              350 pts
            </div>
          </div>
          <button @click="redeemReward(2)" class="mt-2 w-full bg-blue-500 hover:bg-blue-600 text-white py-1.5 rounded text-sm transition-colors">
            Canjear
          </button>
        </div>
  
        <div class="bg-white rounded-lg shadow-md p-3 border-l-4 border-purple-500 opacity-70">
          <div class="flex justify-between items-center">
            <div>
              <h4 class="font-medium">Pase VIP Evento Ambiental</h4>
              <p class="text-xs text-gray-600">Acceso exclusivo a EcoFest 2025</p>
            </div>
            <div class="bg-purple-100 text-purple-800 text-xs font-semibold px-2 py-1 rounded">
              500 pts
            </div>
          </div>
          <div class="mt-2">
            <div class="w-full bg-gray-200 rounded-full h-1.5">
              <div class="bg-purple-500 h-1.5 rounded-full" style="width: 90%"></div>
            </div>
            <p class="text-xs text-right mt-1">¡Te faltan 50 puntos!</p>
          </div>
          <button disabled class="mt-2 w-full bg-gray-300 text-gray-500 py-1.5 rounded text-sm cursor-not-allowed">
            Canjear
          </button>
        </div>
      </div>
  
      <!-- Confetti Animation -->
      <div v-if="showConfetti" class="confetti-container">
        <div v-for="n in 50" :key="n" class="confetti" :style="getRandomConfettiStyle()"></div>
      </div>
  
      <!-- Modal de recompensa -->
      <ModalReward v-if="showRewardModal" @close="showRewardModal = false" />
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import ModalReward from '../modals/ModalReward.vue';
  
  // Estado para modales y animaciones
  const showRewardModal = ref(false);
  const showConfetti = ref(false);
  
  // Función para generar estilos aleatorios para el confeti
  const getRandomConfettiStyle = () => {
    const colors = ['#3CB371', '#4CAF50', '#8BC34A', '#CDDC39', '#FFEB3B'];
    return {
      '--confetti-color': colors[Math.floor(Math.random() * colors.length)],
      '--fall-duration': `${Math.random() * 3 + 2}s`,
      '--fall-delay': `${Math.random() * 2}s`,
      '--left-pos': `${Math.random() * 100}%`,
    };
  };
  
  //  Función para canjear un premio y abrir el modal correctamente
  const redeemReward = (id) => {
    console.log(`Canjeando recompensa con ID: ${id}`); // Debug para ver si la función se llama
    showConfetti.value = true;
    setTimeout(() => {
      showConfetti.value = false;
      showRewardModal.value = true; //  Ahora el modal se activa correctamente
      console.log("Modal abierto: ", showRewardModal.value); // Debug para ver si cambia el estado
    }, 1500);
  };
  </script>
  
  <style scoped>
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
  