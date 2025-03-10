<template>
    <nav class="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200 shadow-lg">
      <div class="flex justify-around max-w-md mx-auto">

        <button @click="$emit('changeScreen', 'home')" class="flex flex-col items-center py-2 px-4">
          <HomeIcon class="h-6 w-6" />
          <span class="text-xs mt-1">Home</span>
        </button>
        <button @click="$emit('changeScreen', 'dashboard')" class="flex flex-col items-center py-2 px-4">
          <ChartPieIcon class="h-6 w-6" />
          <span class="text-xs mt-1">Impacto</span>
        </button>
        <button @click="$emit('changeScreen', 'scanner')" class="flex flex-col items-center py-2 px-4">
          <CameraIcon class="h-6 w-6" />
          <span class="text-xs mt-1">Escanear</span>
        </button>
        <button @click="$emit('changeScreen', 'traceability')" class="flex flex-col items-center py-2 px-4">
          <LinkIcon class="h-6 w-6" />
          <span class="text-xs mt-1">Trazabilidad</span>
        </button>
        <button @click="$emit('changeScreen', 'rewards')" class="flex flex-col items-center py-2 px-4">
          <BellIcon class="h-6 w-6" />
          <span class="text-xs mt-1">Regalos</span>
        </button>
      </div>
    </nav>
</template>

<script setup>
import { Camera as CameraIcon, ChartPie as ChartPieIcon, Home as HomeIcon, Link as LinkIcon, Gift as BellIcon } from 'lucide-vue-next';
</script>
