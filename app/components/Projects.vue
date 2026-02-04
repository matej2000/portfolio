<template>
    <div id="projects" class="h-screen relative flex flex-col pt-20 w-full  bg-[#080d23]">
        <div class="text-white text-9xl z-20 m-auto text-center">PROJECTS</div>
        <div ref="proj_container" class="list_projects flex flex-row flex-nowrap mt-20 ml-10">
            <div v-for="(item, index) in projects" 
            :key="index"
            class="text-white border-black border-t divide-x-1 border-r p-4 text-center">
            
                <div v-if="item.code == 1" class="flex flex-col w-[500px]">
                    
                    <div class="flex flex-col text-2xl h-[200px]">
                        <h1>{{ item.title }}</h1>
                        <p class="text-sm text-blue-400">{{ item.technologies }}</p>
                        <p class="text-lg mt-10">{{ item.description }}</p>
                    </div>
                    <div class="p-2 mt-10 aspect-3/2 object-cover ">
                        <img v-if="index!=3 & index!=4" :src="item.img_path" class="h-[300px] w-full object-cover object-top"/>
                        <img v-else :src="item.img_path" class="h-[300px] w-full object-cover"/>
                    </div>
                </div>
                <div v-else class="flex flex-col w-[500px] h-full mr-10">
                    <div class="m-auto">
                        <h1 class="text-2xl"> Want to see more? Check my Github</h1>
                        <button class="bg-blue-400 w-fit px-3 py-3 rounded-xl mt-5">View more</button>
                    </div>
                </div>
                <!-- <div v-else class="flex flex-col w-[500px]">
                    <div><img  :src="item.img_path" />
                    </div>
                    <div class="flex flex-col text-3xl">
                        <h1>{{ item.title }}</h1>
                        <p>{{ item.description }}</p>
                    </div>
                </div> -->
            </div>

        </div>

    </div>
    <div class="w-full h-screen "></div>
</template>

<script setup>

    import { gsap } from 'gsap';
    import { ScrollTrigger } from 'gsap/ScrollTrigger';
    import {ref, onMounted, useTemplateRef} from 'vue'

    gsap.registerPlugin(ScrollTrigger);
    const proj_container = useTemplateRef("proj_container");

    const projects = [
        // {code: 0},
        {code: 1, title: "Weakly supervised animal detection", img_path: "/images/ws-detr_final-WS_DETR_complex_eng.png", description: "Proposed and implemented improvements to weakly supervised DETR. Conducted a comparative analysis against state-of-the-art weakly supervised frameworks.",technologies: "Python, PyTorch, PytorchLightning, Pandas", link: ""},
        {code: 1, title: "Animal detection dashboard", img_path: "/images/wt.png", description: "Extension of my master's thesis, which enables easy use of models trained during my research.",technologies: "Vue.js, Javascript, Tailwind CSS, Django", link: ""},
        {code: 1, title: "Fantasy premier league assistant", img_path: "/images/fpl_a.png", description: "A dynamic dashboard for Fantasy Premier League managers, built to provide real-time insights. The application interfaces with the official FPL REST API.",technologies: "Vue.js, Javascript, Tailwind CSS", link: "https://www.kaggle.com/competitions/pig-posture-recognition/overview"},
        {code: 1, title: "Slovene sentence paraphrasing", img_path: "/images/slovene.png", description: "Leveraging back-translation techniques to fine-tune a T5 transformer. I engineered a synthetic dataset by translating Gigafida corpus samples into English and back to Slovene.",technologies: "Python, Transformers (HuggingFace), Google Cloud", link: ""},
        {code: 1, title: "Pig posture recognition (Kaggle)", img_path: "/images/ppr.jpeg", description: "This active project serves as a sandbox for implementing advanced feature engineering, hyperparameter optimization, and ensemble modeling techniques to climb the leaderboard.",technologies: "Python, PyTorch, Pandas", link: ""},
        {code: 0, }
        ];

onMounted(() => {
    const el = proj_container.value;
    const scrollAmount = el.scrollWidth - window.innerWidth;
    
    const pausePadding = 50; 

    const tl = gsap.timeline({
        scrollTrigger: {
            trigger: "#projects",
            start: "top top",
            end: () => `+=${scrollAmount + pausePadding}`,
            scrub: 1,
            pin: true,
            anticipatePin: 1,
        }
    });
    tl.to({}, { duration: 0.1 }); 
    tl.to(el, {
        x: -scrollAmount,
        ease: "none"
    });
    tl.to({}, { duration: 0.1 }); 
})
</script>

<style>

</style>