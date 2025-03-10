<template>
  <div class="notifications-screen p-4">
    <h2 class="text-xl font-bold mb-4">Notificaciones</h2>

    <div class="space-y-3">
      <!-- Notificaciones dinámicas -->
      <div v-for="(notification, index) in notifications" :key="index" 
           class="bg-white rounded-lg shadow-md p-4 border-l-4" 
           :class="notification.borderClass">
        <div class="flex">
          <div class="rounded-full p-2 mr-3 flex-shrink-0" :class="notification.bgClass">
            <component :is="notification.icon" class="h-5 w-5" :class="notification.iconColor" />
          </div>
          <div class="flex-1">
            <h4 class="font-medium">{{ notification.title }}</h4>
            <p class="text-sm text-gray-600 mt-1">{{ notification.message }}</p>

            <div v-if="notification.type === 'promo'" class="mt-2">
              <div class="text-xs text-gray-500">Termina en:</div>
              <div class="flex space-x-2 mt-1">
                <div class="bg-gray-100 rounded px-2 py-1 text-center">
                  <div class="text-sm font-bold">{{ timer.hours }}</div>
                  <div class="text-xs">horas</div>
                </div>
                <div class="bg-gray-100 rounded px-2 py-1 text-center">
                  <div class="text-sm font-bold">{{ timer.minutes }}</div>
                  <div class="text-xs">min</div>
                </div>
                <div class="bg-gray-100 rounded px-2 py-1 text-center">
                  <div class="text-sm font-bold">{{ timer.seconds }}</div>
                  <div class="text-xs">seg</div>
                </div>
              </div>
            </div>

            <div v-if="notification.action" class="mt-2">
              <button @click="notification.action.handler" class="text-sm" :class="notification.action.class">
                {{ notification.action.text }}
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { 
  MapPin as MapPinIcon, 
  Gift as GiftIcon, 
  Trophy as TrophyIcon, 
  Bell as BellIcon 
} from 'lucide-vue-next';

// Simulación de datos de notificaciones
const notifications = ref([
  {
    title: "Centro de reciclaje cercano",
    message: "Hay un punto de reciclaje a 300m de tu ubicación actual.",
    icon: MapPinIcon,
    iconColor: "text-green-600",
    bgClass: "bg-green-100",
    borderClass: "border-green-500",
    action: { text: "Ver en mapa", handler: () => alert("Mostrando mapa"), class: "text-green-600 font-medium" }
  },
  {
    title: "Promoción especial",
    message: "¡Recicla 5 envases hoy y obtén puntos dobles!",
    type: "promo",
    icon: GiftIcon,
    iconColor: "text-blue-600",
    bgClass: "bg-blue-100",
    borderClass: "border-blue-500"
  },
  {
    title: "¡Nuevo logro desbloqueado!",
    message: "Has reciclado 10 envases este mes. ¡Sigue así!",
    icon: TrophyIcon,
    iconColor: "text-yellow-600",
    bgClass: "bg-yellow-100",
    borderClass: "border-yellow-500",
    action: { text: "Ver recompensa", handler: () => alert("Mostrando recompensas"), class: "text-yellow-600 font-medium" }
  },
  {
    title: "Recordatorio",
    message: "No has reciclado en los últimos 3 días. ¡Mantén tu racha!",
    icon: BellIcon,
    iconColor: "text-purple-600",
    bgClass: "bg-purple-100",
    borderClass: "border-purple-500",
    action: { text: "Reciclar ahora", handler: () => alert("Abriendo escáner"), class: "mt-2 text-sm bg-purple-500 text-white px-3 py-1 rounded-md" }
  }
]);

// Simulación de un temporizador para la promoción
const timer = ref({ hours: "05", minutes: "23", seconds: "47" });
let timerInterval;

onMounted(() => {
  timerInterval = setInterval(() => {
    let h = parseInt(timer.value.hours);
    let m = parseInt(timer.value.minutes);
    let s = parseInt(timer.value.seconds);

    s--;
    if (s < 0) {
      s = 59;
      m--;
      if (m < 0) {
        m = 59;
        h--;
        if (h < 0) {
          h = 0;
          m = 0;
          s = 0;
          clearInterval(timerInterval);
        }
      }
    }

    timer.value.hours = h.toString().padStart(2, "0");
    timer.value.minutes = m.toString().padStart(2, "0");
    timer.value.seconds = s.toString().padStart(2, "0");
  }, 1000);
});

onUnmounted(() => {
  clearInterval(timerInterval);
});
</script>
