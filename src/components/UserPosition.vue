<template>
    <div class="bg-white rounded-lg shadow-md p-4 mb-4">
      <div class="flex items-center">
        <div class="bg-green-100 p-2 rounded-full mr-3">
          <Trophy class="h-6 w-6 text-green-600" />
        </div>
        <div>
          <h3 class="font-semibold">Tu posición</h3>
          <p class="text-xs text-gray-600">Nivel {{ level }} • {{ xp }} XP</p>
        </div>
        <div class="ml-auto">
          <span class="text-xl font-bold text-green-600">{{ points }} pts</span>
        </div>
      </div>
      <div class="mt-3 h-2 bg-gray-200 rounded-full overflow-hidden">
        <div class="h-full bg-green-500" :style="{ width: `${percentage}%` }"></div>
      </div>
      <div class="flex justify-between text-xs mt-1 text-gray-600">
        <span>0 pts</span>
        <span>1000 pts</span>
      </div>
    </div>
  </template>
  
  <script setup>
  import { Trophy } from 'lucide-vue-next';
  
  defineProps({
    level: {
      type: Number,
      required: true
    },
    xp: {
      type: Number,
      required: true
    },
    points: {
      type: Number,
      required: true
    },
    percentage: {
      type: Number,
      required: true
    }
  });
  </script>