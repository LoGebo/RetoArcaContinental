<template>
    <div class="bg-white rounded-lg shadow-md p-3 mb-4">
      <div class="grid grid-cols-3 gap-2">
        <button 
          v-for="tab in tabs" 
          :key="tab.value" 
          @click="$emit('change-tab', tab.value)"
          :class="[
            'py-2 rounded-md transition-colors text-sm font-medium',
            activeTab === tab.value 
              ? 'bg-green-100 text-green-600' 
              : 'bg-gray-50 text-gray-600 hover:bg-gray-100'
          ]"
        >
          {{ tab.label }}
        </button>
      </div>
    </div>
  </template>
  
  <script setup>
  defineProps({
    tabs: {
      type: Array,
      required: true
    },
    activeTab: {
      type: String,
      required: true
    }
  });
  
  defineEmits(['change-tab']);
  </script>