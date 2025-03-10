<template>
    <div class="bg-white rounded-lg shadow-md p-4 mb-4">
      <div class="flex items-center justify-between mb-3">
        <div class="flex items-center">
          <div class="bg-green-100 p-1.5 rounded-full mr-2">
            <Users class="h-5 w-5 text-green-600" />
          </div>
          <h3 class="font-semibold">Ranking de Amigos</h3>
        </div>
        <button class="text-xs bg-green-50 text-green-600 px-2 py-1 rounded-md border border-green-200 flex items-center">
          <UserPlus class="h-3.5 w-3.5 mr-1" />
          Invitar
        </button>
      </div>
  
      <div class="space-y-3">
        <div v-for="friend in friends" :key="friend.name" 
             :class="[
               'p-3 rounded-lg border-l-4 flex items-center',
               friend.highlight ? 'border-green-500 bg-green-50' : 'border-gray-200'
             ]">
          <div :class="[
            'w-8 h-8 rounded-full flex items-center justify-center font-bold text-sm mr-3',
            friend.position === 1 ? 'bg-yellow-100 text-yellow-700' : 
            friend.position === 2 ? 'bg-gray-200 text-gray-700' : 
            friend.position === 3 ? 'bg-amber-100 text-amber-700' : 
            'bg-gray-100 text-gray-700'
          ]">
            {{ friend.position }}
          </div>
          <div class="h-10 w-10 rounded-full overflow-hidden mr-3">
            <img :src="friend.avatar" :alt="friend.name" class="w-full h-full object-cover" />
          </div>
          <div class="flex-1">
            <div class="flex items-center">
              <div class="font-medium">{{ friend.name }}</div>
              <span v-if="friend.badge" class="ml-2 bg-green-100 text-green-600 text-xs px-2 py-0.5 rounded-md">
                {{ friend.badge }}
              </span>
            </div>
            <div class="text-xs text-gray-600">Nivel {{ friend.level }}</div>
          </div>
          <div class="font-bold text-green-600">{{ friend.points }} pts</div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { Users, UserPlus } from 'lucide-vue-next';
  
  defineProps({
    friends: {
      type: Array,
      required: true
    }
  });
  </script>