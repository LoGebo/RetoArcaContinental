<template>
  <div class="font-sans text-gray-800 bg-gray-50 min-h-screen max-w-md mx-auto relative overflow-hidden">
    <!-- Contenido principal -->
    <main class="pb-20">
      <!-- Información del perfil -->
      <div class="p-4">
        <div class="flex items-start">
          <!-- Foto de perfil -->
          <div class="relative mr-4">
            <div class="w-20 h-20 rounded-full bg-gradient-to-r from-green-400 to-green-600 p-0.5">
              <img src="https://randomuser.me/api/portraits/men/44.jpg" alt="Foto de perfil" class="w-full h-full object-cover rounded-full border-2 border-white" />
            </div>
            <div class="absolute -bottom-1 -right-1 bg-green-500 rounded-full p-1 border-2 border-white">
              <LeafIcon class="h-4 w-4 text-white" />
            </div>
          </div>
          
          <!-- Información del usuario -->
          <div class="flex-1">
            <div class="flex justify-between items-center mb-1">
              <h2 class="text-xl font-bold">gebou</h2>
              <div class="bg-green-100 text-green-800 text-xs font-semibold px-2 py-1 rounded-full">
                Nivel 4
              </div>
            </div>
            <p class="text-sm text-gray-600 mb-2">Jesus Daniel Mtz</p>
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
        
        <!-- Descripción del perfil -->
        <div class="mt-3">
          <p class="text-sm">🌱 Amante del medio ambiente y del fortnite</p>
          <p class="text-sm">🔄 Reciclando desde anoche</p>
          <p class="text-sm">🌍 Monterrey, MX</p>
        </div>
        
        <!-- Botones de acción -->
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
      
      <!-- Estadísticas de reciclaje -->
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
        
        <!-- Gráfico de barras -->
        <div class="h-48 relative">
          <div class="absolute inset-0">
            <div class="h-full flex flex-col justify-between">
              <div v-for="n in 5" :key="n" class="border-t border-gray-100 h-1/5"></div>
            </div>
            
            <div class="absolute inset-0 flex items-end justify-between pt-6 pb-6">
              <div v-for="(item, index) in chartData" :key="index" class="flex flex-col items-center w-1/12">
                <div class="w-full px-0.5">
                  <div class="w-full bg-green-500 rounded-t-sm transition-all duration-500 ease-in-out" :style="{ height: `${(item.value / maxValue) * 100}%` }"></div>
                </div>
                <div class="text-xs text-gray-500 mt-1">{{ item.label }}</div>
              </div>
            </div>
            
            <div class="absolute top-0 left-0 h-full flex flex-col justify-between text-xs text-gray-400 py-6">
              <div>{{ maxValue }}</div>
              <div>{{ Math.round(maxValue * 0.75) }}</div>
              <div>{{ Math.round(maxValue * 0.5) }}</div>
              <div>{{ Math.round(maxValue * 0.25) }}</div>
              <div>0</div>
            </div>
          </div>
        </div>
        
        <div class="flex justify-between items-center mt-2">
          <div class="flex items-center">
            <div class="w-3 h-3 bg-green-500 rounded-sm mr-1"></div>
            <span class="text-xs text-gray-600">Envases reciclados</span>
          </div>
          <div class="text-xs text-gray-600">
            Total: {{ totalRecycled }} envases
          </div>
        </div>
      </div>

       <!-- Actividad reciente -->
       <div class="p-4">
        <h3 class="font-bold mb-3">Actividad Reciente</h3>
        
        <!-- Post de reciclaje -->
        <div class="bg-white rounded-lg shadow-md mb-4">
          <div class="p-3 border-b border-gray-100">
            <div class="flex items-center">
              <img src="https://randomuser.me/api/portraits/men/44.jpg" alt="Foto de perfil" class="w-8 h-8 rounded-full mr-2" />
              <div>
                <div class="font-medium">gebou</div>
                <div class="text-xs text-gray-500">Hace 2 días</div>
              </div>
              <button class="ml-auto">
                <MoreVerticalIcon class="h-5 w-5 text-gray-500" />
              </button>
            </div>
          </div>
          
          <div class="p-3">
            <div class="flex items-center mb-2">
              <div class="bg-green-100 p-2 rounded-full mr-3">
                <RecycleIcon class="h-6 w-6 text-green-600" />
              </div>
              <div>
                <p class="text-sm">¡He reciclado 5 envases hoy! 🌱♻️</p>
              </div>
            </div>
            
            <div class="bg-gray-50 p-3 rounded-lg">
              <div class="flex items-center">
                <div class="bg-green-100 rounded-full p-1.5 mr-2">
                  <PackageIcon class="h-4 w-4 text-green-600" />
                </div>
                <div class="text-sm">
                  <span class="font-medium">5 envases reciclados</span>
                  <div class="text-xs text-gray-500">2.5 kg de CO₂ ahorrados</div>
                </div>
              </div>
            </div>
            
            <div class="flex justify-between mt-3 border-t border-gray-100 pt-3">
              <button class="flex items-center text-gray-500">
                <HeartIcon class="h-5 w-5 mr-1" />
                <span class="text-xs">24</span>
              </button>
              <button class="flex items-center text-gray-500">
                <MessageCircleIcon class="h-5 w-5 mr-1" />
                <span class="text-xs">3</span>
              </button>
              <button class="flex items-center text-gray-500">
                <ShareIcon class="h-5 w-5 mr-1" />
                <span class="text-xs">Compartir</span>
              </button>
            </div>
          </div>
        </div>
        
        <!-- Post de logro -->
        <div class="bg-white rounded-lg shadow-md mb-4">
          <div class="p-3 border-b border-gray-100">
            <div class="flex items-center">
              <img src="https://randomuser.me/api/portraits/men/44.jpg" alt="Foto de perfil" class="w-8 h-8 rounded-full mr-2" />
              <div>
                <div class="font-medium">gebou</div>
                <div class="text-xs text-gray-500">Hace 1 semana</div>
              </div>
              <button class="ml-auto">
                <MoreVerticalIcon class="h-5 w-5 text-gray-500" />
              </button>
            </div>
          </div>
          
          <div class="p-3">
            <div class="flex items-center mb-2">
              <div class="bg-yellow-100 p-2 rounded-full mr-3">
                <TrophyIcon class="h-6 w-6 text-yellow-600" />
              </div>
              <div>
                <p class="text-sm">¡He alcanzado el Nivel 4! 🎉 Gracias a todos por el apoyo.</p>
              </div>
            </div>
            
            <div class="bg-gradient-to-r from-green-50 to-yellow-50 p-3 rounded-lg">
              <div class="flex items-center justify-between">
                <div class="flex items-center">
                  <div class="bg-yellow-100 rounded-full p-1.5 mr-2">
                    <AwardIcon class="h-4 w-4 text-yellow-600" />
                  </div>
                  <div class="text-sm">
                    <span class="font-medium">Nivel 4 desbloqueado</span>
                  </div>
                </div>
                <div class="text-xs font-medium text-green-600">+500 puntos</div>
              </div>
              <div class="mt-2 h-2 bg-gray-200 rounded-full overflow-hidden">
                <div class="h-full bg-gradient-to-r from-green-400 to-green-600 w-3/4"></div>
              </div>
              <div class="flex justify-between text-xs mt-1">
                <span>Nivel 4</span>
                <span>Nivel 5</span>
              </div>
            </div>
            
            <div class="flex justify-between mt-3 border-t border-gray-100 pt-3">
              <button class="flex items-center text-red-500">
                <HeartIcon class="h-5 w-5 mr-1 fill-current" />
                <span class="text-xs">42</span>
              </button>
              <button class="flex items-center text-gray-500">
                <MessageCircleIcon class="h-5 w-5 mr-1" />
                <span class="text-xs">7</span>
              </button>
              <button class="flex items-center text-gray-500">
                <ShareIcon class="h-5 w-5 mr-1" />
                <span class="text-xs">Compartir</span>
              </button>
            </div>
          </div>
        </div>
        
        <!-- Post de visita -->
        <div class="bg-white rounded-lg shadow-md mb-4">
          <div class="p-3 border-b border-gray-100">
            <div class="flex items-center">
              <img src="https://randomuser.me/api/portraits/men/44.jpg" alt="Foto de perfil" class="w-8 h-8 rounded-full mr-2" />
              <div>
                <div class="font-medium">gebou</div>
                <div class="text-xs text-gray-500">Hace 2 semanas</div>
              </div>
              <button class="ml-auto">
                <MoreVerticalIcon class="h-5 w-5 text-gray-500" />
              </button>
            </div>
          </div>
          
          <div class="p-3">
            <div class="flex items-center mb-2">
              <div class="bg-blue-100 p-2 rounded-full mr-3">
                <MapPinIcon class="h-6 w-6 text-blue-600" />
              </div>
              <div>
                <p class="text-sm">Visitando el nuevo centro de reciclaje en el centro. ¡Muy bien organizado! 👏</p>
              </div>
            </div>
            
            <div class="relative h-48 bg-gray-100 rounded-lg overflow-hidden mb-2">
              <!-- Simulación de mapa -->
              <div class="absolute inset-0 bg-green-50">
                <div class="absolute top-1/3 left-1/2 bg-blue-500 rounded-full h-4 w-4 border-2 border-white shadow-md pulse-animation"></div>
                <div class="absolute top-1/2 right-1/3 bg-green-500 rounded-full h-4 w-4 border-2 border-white shadow-md"></div>
                <div class="absolute bottom-1/4 left-1/3 bg-green-500 rounded-full h-4 w-4 border-2 border-white shadow-md"></div>
              </div>
              <div class="absolute bottom-2 left-2 bg-white px-2 py-1 rounded-md text-xs shadow-md">
                Centro de Reciclaje Municipal
              </div>
            </div>
            
            <div class="flex justify-between mt-3 border-t border-gray-100 pt-3">
              <button class="flex items-center text-gray-500">
                <HeartIcon class="h-5 w-5 mr-1" />
                <span class="text-xs">18</span>
              </button>
              <button class="flex items-center text-gray-500">
                <MessageCircleIcon class="h-5 w-5 mr-1" />
                <span class="text-xs">2</span>
              </button>
              <button class="flex items-center text-gray-500">
                <ShareIcon class="h-5 w-5 mr-1" />
                <span class="text-xs">Compartir</span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </main>

    <!-- Barra de navegación inferior -->
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
  ChevronLeft as ChevronLeftIcon,
  Settings as SettingsIcon,
  Leaf as LeafIcon,
  UserPlus as UserPlusIcon,
  Recycle as RecycleIcon,
  Package as PackageIcon,
  Heart as HeartIcon,
  MessageCircle as MessageCircleIcon,
  Share as ShareIcon,
  MoreVertical as MoreVerticalIcon,
  Trophy as TrophyIcon,
  Award as AwardIcon,
  MapPin as MapPinIcon,
  Home as HomeIcon,
  Search as SearchIcon,
  Camera as CameraIcon,
  User as UserIcon,
  Bell as BellIcon
} from 'lucide-vue-next';

// Filtro de tiempo para el gráfico
const timeFilter = ref('3m');

// Datos del gráfico según el filtro seleccionado
const chartData3m = [
  { label: 'Ene', value: 12 },
  { label: 'Feb', value: 18 },
  { label: 'Mar', value: 15 },
  { label: 'Abr', value: 22 },
  { label: 'May', value: 28 },
  { label: 'Jun', value: 24 },
  { label: 'Jul', value: 30 },
  { label: 'Ago', value: 25 },
  { label: 'Sep', value: 32 },
  { label: 'Oct', value: 28 },
  { label: 'Nov', value: 35 },
  { label: 'Dic', value: 40 }
];

const chartData1y = [
  { label: 'Ene', value: 12 },
  { label: 'Feb', value: 18 },
  { label: 'Mar', value: 15 },
  { label: 'Abr', value: 22 },
  { label: 'May', value: 28 },
  { label: 'Jun', value: 24 },
  { label: 'Jul', value: 30 },
  { label: 'Ago', value: 25 },
  { label: 'Sep', value: 32 },
  { label: 'Oct', value: 28 },
  { label: 'Nov', value: 35 },
  { label: 'Dic', value: 40 }
];

const chartDataAll = [
  { label: '2020', value: 45 },
  { label: '2021', value: 78 },
  { label: '2022', value: 120 },
  { label: '2023', value: 156 },
  { label: '2024', value: 95 },
  { label: '', value: 0 },
  { label: '', value: 0 },
  { label: '', value: 0 },
  { label: '', value: 0 },
  { label: '', value: 0 },
  { label: '', value: 0 },
  { label: '', value: 0 }
];

// Datos del gráfico actual
const chartData = ref(chartData3m);
const maxValue = ref(Math.max(...chartData.value.map(item => item.value)) * 1.2);
const totalRecycled = ref(chartData.value.reduce((sum, item) => sum + item.value, 0));

// Cambiar el filtro de tiempo
const setTimeFilter = (filter) => {
  timeFilter.value = filter;
  
  if (filter === '3m') {
    chartData.value = chartData3m;
  } else if (filter === '1y') {
    chartData.value = chartData1y;
  } else {
    chartData.value = chartDataAll;
  }
  
  maxValue.value = Math.max(...chartData.value.map(item => item.value)) * 1.2;
  totalRecycled.value = chartData.value.reduce((sum, item) => sum + item.value, 0);
};

// Función para volver atrás
const goBack = () => {
  // En una app real, esto navegaría hacia atrás
  console.log('Volver atrás');
};
</script>

<style>
/* Animación de pulso para el mapa */
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