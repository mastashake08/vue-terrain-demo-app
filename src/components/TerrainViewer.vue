<template>
  <div class="app">
    <div class="controls">
      <h2>Terrain Generator Controls</h2>

      <div>
        <label>Terrain Size:</label>
        <input type="range" v-model="state.terrainSize" min="1000" max="20000" step="500">
        <span>{{ state.terrainSize }}</span>
      </div>

      <div>
        <label>Segments:</label>
        <input type="range" v-model="state.segments" min="256" max="4096" step="128">
        <span>{{ state.segments }}</span>
      </div>

      <div>
        <label>Height Scaling:</label>
        <input type="range" v-model="state.heightScaling" min="1" max="100" step="1">
        <span>{{ state.heightScaling }}</span>
      </div>

      <div>
        <label>Noise Scale:</label>
        <input type="range" v-model="state.noiseScale" min="0.001" max="0.1" step="0.001">
        <span>{{ state.noiseScale }}</span>
      </div>

      <div>
        <label>Noise Type:</label>
        <select v-model="state.noiseType">
          <option value="simplex">Simplex</option>
          <option value="perlin">Perlin</option>
        </select>
      </div>

      <div>
        <label>Terrain Color:</label>
        <input type="color" v-model="state.terrainColor">
      </div>

      <div>
        <label>Background Color:</label>
        <input type="color" v-model="state.backgroundColor">
      </div>

      <button @click="applySettings">Apply Settings</button>
    </div>

    <div class="viewer">
      <TerrainGenerator 
        v-show="showTerrain"
        :terrainSize="state.terrainSize"
        :segments="state.segments"
        :heightScaling="state.heightScaling"
        :noiseScale="state.noiseScale"
        :terrainColor="state.terrainColor"
        :backgroundColor="state.backgroundColor"
        :noiseType="state.noiseType"
        :texturePaths="{
          albedo: '/textures/albedo.jpg',
          normal: '/textures/normal.jpg',
          roughness: '/textures/roughness.png'
        }"
        ref="terrainRef"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'
import TerrainGenerator from '@mastashake08/terrain-generator'

// Terrain configuration state
const state = reactive({
  terrainSize: 10000,
  segments: 2048,
  heightScaling: 10,
  noiseScale: 0.04,
  terrainColor: "#87CEEB",
  backgroundColor: "#000000",
  noiseType: "simplex"
})

const terrainRef = ref(null)
const showTerrain = ref(false)
// Function to apply settings dynamically
const applySettings = () => {
  if (terrainRef.value) {
    
    showTerrain.value = true
  }
}
</script>

<style scoped>
.app {
  display: flex;
  height: 100vh;
  width: 100vw;
}

.controls {
  padding: 20px;
  width: 300px;
  background-color: #222;
  color: white;
  overflow-y: auto;
}

.controls input,
.controls select {
  margin-bottom: 10px;
  width: 100%;
}

.viewer {
  flex-grow: 1;
  height: 100vh;
  width: 100%;
}
</style>
