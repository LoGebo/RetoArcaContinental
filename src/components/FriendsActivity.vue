<template>
    <div class="bg-white rounded-lg shadow-md p-4">
      <div class="flex items-center mb-3">
        <div class="bg-green-100 p-1.5 rounded-full mr-2">
          <Activity class="h-5 w-5 text-green-600" />
        </div>
        <h3 class="font-semibold">Actividad Reciente</h3>
      </div>
  
      <div class="space-y-3">
        <div v-for="activity in activities" :key="activity.time" 
             :class="[
               'p-3 rounded-lg border',
               activity.highlight ? 'border-green-200 bg-green-50' : 'border-gray-200'
             ]">
          <div class="flex items-center">
            <div class="h-9 w-9 rounded-full overflow-hidden mr-3">
              <img :src="activity.avatar" :alt="activity.name" class="w-full h-full object-cover" />
            </div>
            <div class="flex-1">
              <div class="text-sm">
                <span class="font-medium">{{ activity.name }}</span> {{ activity.action }}
              </div>
              <div class="flex justify-between items-center mt-1">
                <div class="text-xs text-gray-600">{{ activity.time }}</div>
                <div class="text-xs font-medium text-green-600">{{ activity.points }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { Activity } from 'lucide-vue-next';
  
  defineProps({
    activities: {
      type: Array,
      required: true
    }
  });
  </script>