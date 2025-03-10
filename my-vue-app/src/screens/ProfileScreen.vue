<template>
    <div class="font-sans text-gray-800 bg-gray-50 min-h-screen max-w-md mx-auto relative overflow-hidden">
      <!-- Main Content -->
      <main class="pb-20">
        <!-- Profile Information -->
        <div class="p-4">
          <div class="flex items-start">
            <!-- Profile Picture -->
            <div class="relative mr-4">
              <div class="w-20 h-20 rounded-full bg-gradient-to-r from-green-400 to-green-600 p-0.5">
                <img src="https://randomuser.me/api/portraits/women/44.jpg" alt="Foto de perfil" class="w-full h-full object-cover rounded-full border-2 border-white" />
              </div>
              <div class="absolute -bottom-1 -right-1 bg-green-500 rounded-full p-1 border-2 border-white">
                <LeafIcon class="h-4 w-4 text-white" />
              </div>
            </div>
            
            <!-- User Information -->
            <div class="flex-1">
              <div class="flex justify-between items-center mb-1">
                <h2 class="text-xl font-bold">mariasanchez</h2>
                <div class="bg-green-100 text-green-800 text-xs font-semibold px-2 py-1 rounded-full">
                  Nivel 4
                </div>
              </div>
              <p class="text-sm text-gray-600 mb-2">María Sánchez</p>
              <div class="flex space-x-4 text-center text-sm">
                <div>
                  <div class="font-bold">156</div>
                  <div class="text-xs text-gray-600">Reciclajes</div>
                </div>
                <div>
                  <div class="font-bold">243</div>
                  <div class="text-xs text-gray-600">Seguidores</div>
                </div>
                <div>
                  <div class="font-bold">185</div>
                  <div class="text-xs text-gray-600">Siguiendo</div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Profile Description -->
          <div class="mt-3">
            <p class="text-sm">🌱 Amante del medio ambiente y activista por un mundo más limpio</p>
            <p class="text-sm">🔄 Reciclando desde 2023</p>
            <p class="text-sm">🌍 Madrid, España</p>
          </div>
          
          <!-- Action Buttons -->
          <div class="flex space-x-2 mt-3">
            <button class="flex-1 bg-green-500 hover:bg-green-600 text-white py-1.5 rounded-md text-sm font-medium transition-colors">
              Editar perfil
            </button>
            <button class="flex-1 bg-white border border-gray-300 py-1.5 rounded-md text-sm font-medium transition-colors">
              Compartir perfil
            </button>
            <button class="bg-white border border-gray-300 p-1.5 rounded-md">
              <UserPlusIcon class="h-5 w-5" />
            </button>
            <button class="bg-white border border-gray-300 p-1.5 rounded-md">
              <SettingsIcon class="h-5 w-5" />
            </button>
          </div>
        </div>
        
        <!-- Recycling Statistics -->
        <div class="bg-white p-4 border-t border-b border-gray-200">
          <div class="flex justify-between items-center mb-3">
            <h3 class="font-bold">Estadísticas de Reciclaje</h3>
            <div class="flex bg-gray-100 rounded-lg overflow-hidden text-xs">
              <button @click="setTimeFilter('3m')" class="px-3 py-1.5" :class="timeFilter === '3m' ? 'bg-green-500 text-white' : 'text-gray-600'">
                3 meses
              </button>
              <button @click="setTimeFilter('1y')" class="px-3 py-1.5" :class="timeFilter === '1y' ? 'bg-green-500 text-white' : 'text-gray-600'">
                Año
              </button>
              <button @click="setTimeFilter('all')" class="px-3 py-1.5" :class="timeFilter === 'all' ? 'bg-green-500 text-white' : 'text-gray-600'">
                Todo
              </button>
            </div>
          </div>
        </div>
      </main>
  
      <!-- Bottom Navigation Bar -->
      <nav class="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200 shadow-lg">
        <div class="flex justify-around max-w-md mx-auto">
          <button class="flex flex-col items-center py-2 px-4 text-gray-600">
            <HomeIcon class="h-6 w-6" />
            <span class="text-xs mt-1">Inicio</span>
          </button>
          <button class="flex flex-col items-center py-2 px-4 text-gray-600">
            <SearchIcon class="h-6 w-6" />
            <span class="text-xs mt-1">Explorar</span>
          </button>
          <button class="flex flex-col items-center py-2 px-4 text-gray-600">
            <CameraIcon class="h-6 w-6" />
            <span class="text-xs mt-1">Escanear</span>
          </button>
          <button class="flex flex-col items-center py-2 px-4 text-gray-600">
            <TrophyIcon class="h-6 w-6" />
            <span class="text-xs mt-1">Premios</span>
          </button>
          <button class="flex flex-col items-center py-2 px-4 text-green-600">
            <UserIcon class="h-6 w-6" />
            <span class="text-xs mt-1">Perfil</span>
          </button>
        </div>
      </nav>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { 
    Leaf as LeafIcon,
    UserPlus as UserPlusIcon,
    Home as HomeIcon,
    Search as SearchIcon,
    Camera as CameraIcon,
    Trophy as TrophyIcon,
    User as UserIcon,
    Settings as SettingsIcon
  } from 'lucide-vue-next';
  
  // Time filter for chart
  const timeFilter = ref('3m');
  
  // Go back function
  const goBack = () => {
    console.log('Going back');
  };
  </script>
  
  <style>
  /* Pulse Animation for Map */
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
    background: rgba(59, 130, 246, 0.4);
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
  </style>
  