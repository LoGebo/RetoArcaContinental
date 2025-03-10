<template>
    <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4">
      <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-xs">
        <div class="text-center">
          <div class="mx-auto bg-green-100 rounded-full p-3 w-16 h-16 flex items-center justify-center mb-4">
            <CheckIcon class="h-8 w-8 text-green-600" />
          </div>
          <h3 class="text-xl font-bold mb-2">¡Recompensa Canjeada!</h3>
          <p class="text-gray-600 mb-4">Tu recompensa ha sido añadida a tu cuenta. Revisa tu correo para más detalles.</p>
          <button @click="$emit('close')" class="w-full bg-green-500 hover:bg-green-600 text-white py-2 rounded-lg transition-colors">
            Entendido
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineEmits } from 'vue';
  import { Check as CheckIcon } from 'lucide-vue-next';
  
  // Definir evento para cerrar el modal
  defineEmits(['close']);
  </script>
  