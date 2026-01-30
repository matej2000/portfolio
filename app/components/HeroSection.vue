<template>
  <div ref="scrollTrack" class="relative h-[250vh]">
    <div class="absolute text-white z-10 top-[30vh] left-[5vw] text-8xl"> 
        <h1 class="text-5xl text-[#6366f1]">Hello, I'm </h1>
        <h1 class="text-8xl">Matej Vatovec</h1>
        <h1 class="text-5xl mt-10"> Software developer</h1>
        <h1 class="text-5xl"> Data scientis</h1>
    </div>
    <div class="sticky top-0 w-full h-screen">
      <TresCanvas clear-color="#080d23">
        <TresPerspectiveCamera :position="[-4, 2, motion]" />
        <TresAmbientLight :intensity="1" />
        <Knot />
        <Floor />
        <TresDirectionalLight :position="[0, 2, 4]" :intensity="1.2" cast-shadow />
      </TresCanvas>
    </div>
  </div>

  <section id="experience" class="h-screen bg-[#080d23] flex items-center justify-center -mt-1" ref="target">
    <h2 class="text-black text-4xl">The camera has stopped. Now you scroll the page!</h2>
  </section>
  <!-- <div class="w-full h-full">
   To je test
  </div> -->
  
</template>

<script setup>
  import {ref, onMounted} from 'vue'
  const motion = ref(20)

  const moveCamera = () => {
    motion.value = 10 
  }

  const handleScroll = () => {
    motion.value = Math.max(Math.min(20, 20 - window.scrollY / 50), 20 - 1380 / 50)
  }

  onMounted(() => {
    window.addEventListener("scroll", handleScroll)
  })
</script>