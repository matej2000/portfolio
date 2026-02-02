<template>
  <div ref="mainContainer" class="overflow-hidden relative -mt-1">
    
    <div id="experience" class="relative h-screen bg-[#080d23] flex items-center justify-center overflow-hidden">
      <div class="m-auto flex flex-col">
        <h2 ref="mybox" class="text-white text-9xl">EXPERIENCE</h2>
        <h1 ref="myboxC" class="text-white bg-[#080d23] text-9xl z-20 leading-[0.75]">EXPERIENCE</h1>
        <h2 ref="mybox2" class="text-white text-9xl">EXPERIENCE</h2>
      </div>
          <div 
      v-for="(item, index) in experienceData" 
      :key="index"
      ref="sectionRefs"
      :style="{backgroundColor: item.color, height: item.height}"
      class="experience-sec w-full flex  z-30 absolute bottom-0"
    >
      <div class="flex flex-col text-white ml-[10vw]">
        <h2 class="text-3xl text-blue-400">{{ item.date }}</h2>
        <h1 class="text-5xl font-bold">{{ item.title }}</h1>
        <p class="mt-4 text-xl opacity-80">{{ item.description }}</p>
      </div>
    </div>
    <div ref="sectionLast" class="w-full flex bg-[#080d23] z-30 absolute bottom-0 h-[30vh]">

    </div>
    </div>
    <!-- bg-[#333644] -->

  </div>
</template>

<script setup>
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  import {ref, onMounted, useTemplateRef} from 'vue'

  
  const experienceData = [
  { date: '2022-2025', title: 'Masters of Computer Science', description: 'Advanced algorithms and AI research.' , color: '#333644', height: '60vh'},
  { date: '2020-2022', title: 'Frontend Developer', description: 'Built interactive UIs using Vue and GSAP.', color: '#3b3f4f', height: '50vh'},
  { date: '2018-2020', title: 'Junior Dev', description: 'Started the journey into the world of web.', color: '#45495c', height: '40vh'},
  ];
  const sections = useTemplateRef('sections');

  const myBox = useTemplateRef('mybox');
  const myBox2 = useTemplateRef('mybox2');
  const myBoxC = useTemplateRef('myboxC');

  const sectionRefs = useTemplateRef('sectionRefs');
  const sectionLast = useTemplateRef('sectionLast');
  gsap.registerPlugin(ScrollTrigger);



  onMounted(() => {
  gsap.set(sectionRefs.value, { yPercent: 100 });
  gsap.set(sectionLast.value, {yPercent: 100})

  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: "#experience",
      start: "top top",
      end: `+=${(experienceData.length + 1) * 100}%`,
      scrub: 1,
      pin: true,
      pinSpacing: true,
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

  tl.to(myBox.value, { opacity: 0})
    .to(myBox2.value, { opacity: 0}, "<")
  
  tl.to(myBoxC.value, {y: -300})


  sectionRefs.value.forEach((sec, i) => {
    tl.to(sec, {
      yPercent: 0 ,
      duration: 1,
      ease: "none"
    
    });
    tl.to({}, { duration: 1 }); 

  });
  tl.to(sectionLast.value, {yPercent: 0, duration:1})
  tl.to({}, {duration: 1});

  })


</script>

<style scoped>
:global(body) {
  margin: 0;
  overflow-x: hidden;
}
</style>