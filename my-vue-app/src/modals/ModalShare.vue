<script setup>
import { defineProps, defineEmits } from 'vue';
import { Share as ShareIcon, MessageSquare as MessageSquareIcon, Mail as MailIcon } from 'lucide-vue-next';

defineProps({
  isOpen: Boolean
});

const emit = defineEmits(["close"]);
</script>

<template>
  <div v-if="isOpen" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4">
    <div class="bg-white rounded-lg shadow-xl p-6 w-full max-w-xs">
      <div class="text-center">
        <h3 class="text-xl font-bold mb-4">Compartir mi impacto</h3>
        <div class="bg-green-50 p-4 rounded-lg mb-4">
          <p class="font-medium">¡He reciclado 15 envases este mes!</p>
          <p class="text-sm mt-1">He ahorrado 2.5 kg de CO₂ y contribuido a un planeta más limpio con EcoRecicla.</p>
        </div>
        <div class="flex justify-center space-x-4 mb-4">
          <button class="bg-blue-500 text-white p-2 rounded-full">
            <ShareIcon class="h-6 w-6" />
          </button>
          <button class="bg-green-500 text-white p-2 rounded-full">
            <MessageSquareIcon class="h-6 w-6" />
          </button>
          <button class="bg-red-500 text-white p-2 rounded-full">
            <MailIcon class="h-6 w-6" />
          </button>
        </div>
        <button @click="emit('close')" class="w-full border border-gray-300 py-2 rounded-lg transition-colors">
          Cancelar
        </button>
      </div>
    </div>
  </div>
</template>
