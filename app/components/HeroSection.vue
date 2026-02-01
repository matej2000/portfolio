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
        <TresPerspectiveCamera :position="[x, 2, motion]" :rotation="[0, rotationY, 0]"/>
        <TresAmbientLight :intensity="1" />
        <Knot />
        <Floor />
        <TresDirectionalLight :position="[0, 2, 4]" :intensity="1.2" cast-shadow />
      </TresCanvas>
    </div>
    <div id="about_me" class="absolute bottom-0 h-screen text-white z-20 left-[5vw] pt-10"> 
      <h1 class="text-8xl">About me</h1>
      <!-- <p>
        Software developer with an interest for artificial inteligence. 
        Recently finished my masters degree at the university of Computer and information science.
        I am also able to speak three languages: Slovenian, English and Italian
      </p> -->
    </div>
  </div>
  <section></section>
  
</template>

<script setup>
  import {ref, onMounted} from 'vue'
  const motion = ref(20)
  const x = ref(-4)
  const xS = -4
  const rotationY = ref(0)

  const moveCamera = () => {
    motion.value = 10 
  }

  const handleScroll = () => {
    motion.value = Math.max(Math.min(20, 20 - window.scrollY / 50), 20 - 1380 / 50)
  }

  const handleScroll2 = () => {
    console.log(x.value, motion.value)
    if(window.scrollY < 1380){
      x.value = Math.max(Math.min(-4, xS -(Math.sin((Math.PI/2) * ((window.scrollY)/1380)) *20 )), -24)
      motion.value = Math.max(Math.min(20, (Math.cos((Math.PI/2) * ((window.scrollY)/1180)) * 20) ), -4)
      rotationY.value = -(Math.PI/2) * ((window.scrollY)/1380)};
  }



  onMounted(() => {
    window.addEventListener("scroll", handleScroll2);
  })

</script>