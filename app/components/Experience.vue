<template>
  <div id="experience" class="relative h-screen bg-[#080d23] flex items-center justify-center -mt-1">
    <div class="m-auto flex flex-col overflow-hidden">
      <h2 ref="mybox" class="text-white text-9xl">EXPERIENCE</h2>
      <h1 class="text-white bg-[#080d23] text-9xl z-20 leading-[0.75]">EXPERIENCE</h1>
      <h2 ref="mybox2" class="text-white text-9xl">EXPERIENCE</h2>
    </div>
  </div>
  <div class="w-full h-screen">

  </div>
</template>

<script setup>
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import {ref, onMounted, useTemplateRef} from 'vue'


  const myBox = useTemplateRef('mybox');
  const myBox2 = useTemplateRef('mybox2');
  gsap.registerPlugin(ScrollTrigger);



  onMounted(() => {

  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: "#experience",
      start: "top top",
      end: "+=1500",
      scrub: 1,
      pin: true,
      pinSpacing: true
    }
  });
  
  tl.fromTo(myBox.value, 
    { opacity: 0, x: '20vw' }, 
    { opacity: 1, x: 0, duration: 1 }
  )
  .fromTo(myBox2.value, 
    { opacity: 0, x: '-20vw' }, 
    { opacity: 1, x: 0, duration: 1 }, 
    "<"
  );

  // small pause in the middle
  tl.to({}, { duration: 0.5 });

  tl.to(myBox.value, { y: 100, duration: 1 })
    .to(myBox2.value, { y: -100, duration: 1 }, "<")

  })

</script>

<style>

</style>