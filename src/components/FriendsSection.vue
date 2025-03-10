<template>
    <div class="friends-section">
      <h2 class="text-xl font-bold mb-4">Comunidad Ecológica</h2>
      
      <!-- Tabs de amigos -->
      <FriendsTabs 
        :tabs="friendsTabs" 
        :activeTab="activeFriendsTab" 
        @change-tab="activeFriendsTab = $event" 
      />
  
      <!-- User's Position -->
      <UserPosition 
        :level="4" 
        :xp="350" 
        :points="780" 
        :percentage="70" 
      />
  
      <!-- Friends Leaderboard -->
      <FriendsLeaderboard :friends="friends" />
  
      <!-- Friend Activity -->
      <FriendsActivity :activities="activities" />
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import FriendsTabs from './FriendsTabs.vue';
  import UserPosition from './UserPosition.vue';
  import FriendsLeaderboard from './FriendsLeaderboard.vue';
  import FriendsActivity from './FriendsActivity.vue';
  
  // Tabs de la sección de amigos
  const activeFriendsTab = ref('amigos');
  const friendsTabs = [
    { label: 'Amigos', value: 'amigos' },
    { label: 'Colonia', value: 'colonia' },
    { label: 'Estado', value: 'estado' }
  ];
  
  // Datos para la pantalla de amigos
  const friends = [
    { position: 1, name: 'Ana García', avatar: 'https://placehold.co/40x40', points: 1250, level: 6, highlight: false, badge: 'Líder' },
    { position: 2, name: 'Carlos Mendez', avatar: 'https://placehold.co/40x40', points: 920, level: 5, highlight: false },
    { position: 3, name: 'Tú', avatar: 'https://placehold.co/40x40', points: 780, level: 4, highlight: true },
    { position: 4, name: 'Laura Torres', avatar: 'https://placehold.co/40x40', points: 650, level: 4, highlight: false },
    { position: 5, name: 'Miguel Ángel', avatar: 'https://placehold.co/40x40', points: 520, level: 3, highlight: false, badge: 'Nuevo' }
  ];
  
  // Datos de actividad reciente
  const activities = [
    { name: 'Ana García', avatar: 'https://placehold.co/40x40', action: 'recicló 3 envases', time: 'Hace 20 minutos', points: '+30 pts' },
    { name: 'Carlos Mendez', avatar: 'https://placehold.co/40x40', action: 'subió a Nivel 5', time: 'Hace 2 horas', points: '+100 pts', highlight: true },
    { name: 'Laura Torres', avatar: 'https://placehold.co/40x40', action: 'visitó un centro de reciclaje', time: 'Hace 5 horas', points: '+50 pts' }
  ];
  </script>