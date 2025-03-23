<template>
  <div>
    <TerrainGenerator 
      :terrainSize="1500"
      :segments="4096"
      :heightScaling="100"
      noiseType="simplex"
      :noiseScale="0.04"
      terrainColor="#000"
      backgroundColor="#FFF"
     
    />
  </div>
</template>

<script setup lang="ts">
import TerrainGenerator from '@mastashake08/terrain-generator'
</script>

<style scoped>
div {
  height: 100vh;
  width: 100vw;
}
</style>

