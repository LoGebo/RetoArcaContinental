<template>
    <div class="impact-screen">
      <div class="header">
        <h1 class="text-2xl font-bold text-gray-800">Tu Impacto</h1>
      </div>
      
      <!-- Progress Section -->
      <div class="card">
        <h2 class="card-title">Progreso Mensual</h2>
        <div class="progress-container">
          <div class="progress-chart">
            <div class="progress-circle">
              <svg width="120" height="120" viewBox="0 0 120 120">
                <circle cx="60" cy="60" r="54" fill="none" stroke="#e6e6e6" stroke-width="12" />
                <circle 
                  cx="60" 
                  cy="60" 
                  r="54" 
                  fill="none" 
                  stroke="#4CAF50" 
                  stroke-width="12" 
                  stroke-dasharray="339.292"
                  stroke-dashoffset="135.7168" 
                  transform="rotate(-90 60 60)" 
                />
                <text x="60" y="65" text-anchor="middle" class="progress-text">30/50</text>
              </svg>
            </div>
            <div class="progress-info">
              <h3 class="text-lg font-semibold">Envases Reciclados</h3>
              <p class="text-green-600">Estás un 20% arriba del promedio de tu colonia</p>
            </div>
          </div>
        </div>
      </div>
      
      <!-- CO2 Saved Section -->
      <div class="card">
        <h2 class="card-title">CO2 Ahorrado</h2>
        <div class="co2-container">
          <div class="co2-visual">
            <div class="trees-container">
              <div v-for="i in 3" :key="i" class="tree" :class="`tree-${i}`">
                <tree-icon class="w-12 h-12 text-green-600" />
              </div>
            </div>
          </div>
          <div class="co2-info">
            <h3 class="text-lg font-semibold">Equivalente a 3 árboles salvados</h3>
            <p>Has ahorrado 15kg de CO2 este mes</p>
          </div>
        </div>
      </div>
      
      <!-- Recycling Centers Map -->
      <div class="card">
        <h2 class="card-title">Centros de Reciclaje Cercanos</h2>
        <div class="map-container">
          <div class="map">
            <!-- Placeholder for map -->
            <div class="map-placeholder">
              <map-pin-icon class="w-8 h-8 text-green-500" />
            </div>
          </div>
          
          <!-- Map Filters -->
          <div class="map-filters">
            <button class="filter-btn active">Todos</button>
            <button class="filter-btn">Plástico</button>
            <button class="filter-btn">Vidrio</button>
            <button class="filter-btn">Papel</button>
          </div>
          
          <!-- Nearest Center -->
          <div class="nearest-center">
            <div class="center-info">
              <h3 class="text-lg font-semibold">EcoPunto Centro</h3>
              <p>A 0.5 km - Ocupación: 45%</p>
            </div>
            <button class="directions-btn">
              <navigation-icon class="w-5 h-5" />
              Ir
            </button>
          </div>
        </div>
      </div>
      
      <!-- Share Impact Button -->
      <button class="share-btn">
        <share-icon class="w-5 h-5 mr-2" />
        Compartir mi impacto
      </button>
    </div>
  </template>
  
  <script setup>
  import { 
    Tree as TreeIcon, 
    MapPin as MapPinIcon, 
    Navigation as NavigationIcon,
    Share as ShareIcon
  } from 'lucide-vue-next';
  
  defineEmits(['navigate']);
  </script>
  
  <style scoped>
  .impact-screen {
    padding: 20px;
    height: 100%;
    overflow-y: auto;
  }
  
  .header {
    margin-bottom: 20px;
  }
  
  .card {
    background-color: white;
    border-radius: 16px;
    padding: 16px;
    margin-bottom: 20px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  }
  
  .card-title {
    font-size: 18px;
    font-weight: 600;
    color: #333;
    margin-bottom: 12px;
  }
  
  .progress-container {
    display: flex;
    justify-content: center;
  }
  
  .progress-chart {
    display: flex;
    align-items: center;
    flex-direction: column;
  }
  
  .progress-circle {
    position: relative;
    margin-bottom: 16px;
  }
  
  .progress-text {
    font-size: 18px;
    font-weight: bold;
    fill: #333;
  }
  
  .progress-info {
    text-align: center;
  }
  
  .co2-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .co2-visual {
    margin-bottom: 16px;
    position: relative;
    height: 100px;
    width: 100%;
  }
  
  .trees-container {
    display: flex;
    justify-content: center;
    position: relative;
    height: 100%;
  }
  
  .tree {
    position: absolute;
    bottom: 0;
  }
  
  .tree-1 {
    left: 30%;
    transform: scale(0.9);
  }
  
  .tree-2 {
    left: 50%;
    transform: translateX(-50%) scale(1.1);
  }
  
  .tree-3 {
    right: 30%;
    transform: scale(0.9);
  }
  
  .co2-info {
    text-align: center;
  }
  
  .map-container {
    display: flex;
    flex-direction: column;
  }
  
  .map {
    height: 180px;
    background-color: #f0f0f0;
    border-radius: 12px;
    margin-bottom: 12px;
    position: relative;
    overflow: hidden;
  }
  
  .map-placeholder {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-image: url('/placeholder.svg?height=180&width=350');
    background-size: cover;
  }
  
  .map-filters {
    display: flex;
    overflow-x: auto;
    gap: 8px;
    margin-bottom: 12px;
    padding-bottom: 4px;
  }
  
  .filter-btn {
    padding: 6px 12px;
    border-radius: 20px;
    background-color: #f0f0f0;
    font-size: 14px;
    white-space: nowrap;
  }
  
  .filter-btn.active {
    background-color: #4CAF50;
    color: white;
  }
  
  .nearest-center {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px;
    background-color: #f9f9f9;
    border-radius: 12px;
  }
  
  .directions-btn {
    display: flex;
    align-items: center;
    padding: 8px 16px;
    background-color: #4CAF50;
    color: white;
    border-radius: 20px;
    font-weight: 500;
  }
  
  .share-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    padding: 14px;
    background-color: #4CAF50;
    color: white;
    border-radius: 12px;
    font-weight: 600;
    margin-top: 10px;
  }
  </style>