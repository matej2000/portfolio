<template>
  <TresCanvas window-size clear-color="#080d23" class="w-full h-full">
    <TresPerspectiveCamera :position="[0, 0, 20]" />
    <TresAmbientLight :intensity="1" />
    
    <Knot />
    <Floor />
    <TresDirectionalLight :position="[0, 2, 4]" :intensity="1.2" cast-shadow />
  </TresCanvas>
</template>

<script setup>
</script>