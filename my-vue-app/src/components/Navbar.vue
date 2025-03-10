<template>
  <nav class="bg-gradient-to-r from-green-500 to-emerald-600 text-white p-4 shadow-md">
    <div class="flex justify-between items-center">
      <div class="flex items-center">
        <RecycleIcon class="h-6 w-6 mr-2" />
        <h1 class="text-xl font-bold">EcoChain</h1>
      </div>
      <div class="flex items-center space-x-4">
        <!-- Notifications Button -->
        <button class="relative" @click="$emit('changeScreen', 'notifications')">
          <BellIcon class="h-6 w-6" />
          <span class="absolute -top-1 -right-1 bg-red-500 text-white text-xs rounded-full h-4 w-4 flex items-center justify-center">3</span>
        </button>

        <!-- Profile Button -->
        <button @click="$emit('changeScreen', 'profile')">
          <UserIcon class="h-6 w-6" />
        </button>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { BellIcon, UserIcon, Recycle as RecycleIcon } from 'lucide-vue-next';
</script>
