<template>
           
    <div @mouseenter="playAnim" @mouseleave="pauseAnim" class="max-w-[2000px] m-auto">
          
        <div v-show="visible" ref="div_hover" class="text-white text-5xl font-bold text-center p-5 cursor-pointer">
            {{ title }}
        </div>
        <div v-show="!visible" class="marquee-window overflow-hidden" ref="container">
            <div class="marquee-wrapper flex w-max" ref="wrapper">
                <div v-for="(item, index) in logos" :key="'a-' + index" class="marquee-content p-5">
                <div class="py-4 px-10 bg-white/10">
                        <div v-html="item" class="w-[80px] h-[80px] fill-white flex items-center justify-center"></div>
                    </div>
                </div>
                <div v-for="(item, index) in logos" :key="'b-' + index" class="marquee-content p-5">
                    <div class="py-4 px-10 bg-white/10">
                        <div v-html="item" class="w-[80px] h-[80px] fill-white flex items-center justify-center"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

import { gsap } from 'gsap';
import {ref, onMounted, onUnmounted, useTemplateRef, nextTick} from 'vue'

const props = defineProps({
  title: {
    type: String,
    default: 'Category Name'
  },
  skills: {
    type: Array,
    default: () => []
  },
  logos: {
    type: Array,
    default: () => []
  }
});

const wrapper = useTemplateRef("wrapper")
let tween = null;
let visible = ref(true);


onMounted(() => {

    const dynamicDuration = (props.logos.length ) * 2;

    tween = gsap.to(wrapper.value, {
        xPercent: -50,
        ease: "none",
        duration: dynamicDuration,
        repeat: -1,
    });
    
    gsap.set(tween, { timeScale: 0 });
})

const playAnim = () => {
    visible.value = false;
    if (tween) gsap.to(tween, { timeScale: 1, duration: 0.5, overwrite: true });
};

const pauseAnim = () => {
    visible.value = true;
    if (tween) gsap.to(tween, { timeScale: 0, duration: 0.5, overwrite: true });
};

onUnmounted(() => {
  if (tween) tween.kill();
});

</script>