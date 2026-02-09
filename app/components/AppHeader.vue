<template>
  <!-- Include this script tag or install `@tailwindplus/elements` via npm: -->
    <!-- <script src="https://cdn.jsdelivr.net/npm/@tailwindplus/elements@1" type="module"></script> -->
    <nav class="fixed top-0 z-50 w-full backdrop-blur-xl bg-[#080d23]/70">
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
        <div class="relative flex h-16 items-center justify-between">
            <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
                <!-- Mobile menu button-->
                <button type="button" @click="mobile_menu =  !mobile_menu" class="relative inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:bg-white/5 hover:text-white focus:outline-2 focus:-outline-offset-1 focus:outline-indigo-500">
                <span class="absolute -inset-0.5"></span>
                <span class="sr-only">Open main menu</span>
                <svg viewBox="0 0 24 24"  fill="none" stroke="currentColor" stroke-width="1.5" data-slot="icon" aria-hidden="true" class="size-6 in-aria-expanded:hidden">
                    <path d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" stroke-linecap="round" stroke-linejoin="round" />
                </svg>
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" data-slot="icon" aria-hidden="true" class="size-6 hidden">
                    <path d="M6 18 18 6M6 6l12 12" stroke-linecap="round" stroke-linejoin="round" />
                </svg>
                </button>
            </div>
            <div class="flex flex-1 items-center justify-center sm:items-stretch">
                <div class="hidden sm:ml-6 sm:block">
                <div class="flex space-x-4">
                    <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-white/5 hover:text-white" -->
                    <a href="#about_me" class="rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-white/5 hover:text-white">About me</a>
                    <a href="#experience" class="rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-white/5 hover:text-white">Experience</a>
                    <a href="#projects" class="rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-white/5 hover:text-white">Projects</a>
                    <a href="#skills" class="rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-white/5 hover:text-white">Skills</a>
                </div>
                </div>
            </div>
        
        </div>
    </div>

    <div v-show="mobile_menu" class="flex z-20 flex-row w-screen h-screen absolute top-0 left-0">
        <div class="flex flex-col basis-1/2 bg-white px-2">
            <div class="flex flex-row justify-end items-center mt-4 px-3 border-b-1 border-gray-300 pb-1">
                <div>
                    <button @click="mobile_menu = false" class="w-fit h-fit text-white cursor-pointer bg-white border-gray-100 hover:bg-gray-200 focus:ring-4 focus:outline-none font-medium rounded-full text-sm p-1 text-center inline-flex items-center ">
                        <span class="sr-only">Close menu</span>
                        <svg class="h-5 w-5 text-black" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                        </svg>
                    </button>
                </div>
            </div>
            <div class="items-center m-auto w-full text-xl text-center">
                <a @click="mobile_menu = false" href="#about_me" class="hover:bg-black hover:text-white mb-5 block rounded-md py-2 font-bold">About me</a>
                <a @click="mobile_menu = false" href="/#experience" class="hover:bg-black hover:text-white mb-5 block rounded-md py-2 font-bold">Experience</a>
                <a @click="mobile_menu = false" href="/#projects" class="hover:bg-black hover:text-white mb-5 block rounded-md py-2 font-bold">Project</a>
                <a @click="mobile_menu = false" href="/skills" class="hover:bg-black hover:text-white mb-5 block rounded-md py-2 font-bold">Skills</a>           

            </div>
            <div class="flex flex-row justify-center text-md pb-3 cursor-pointer">
                <div class="flex flex-row">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-5 mr-2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M7.217 10.907a2.25 2.25 0 1 0 0 2.186m0-2.186c.18.324.283.696.283 1.093s-.103.77-.283 1.093m0-2.186 9.566-5.314m-9.566 7.5 9.566 5.314m0 0a2.25 2.25 0 1 0 3.935 2.186 2.25 2.25 0 0 0-3.935-2.186Zm0-12.814a2.25 2.25 0 1 0 3.933-2.185 2.25 2.25 0 0 0-3.933 2.185Z" />
                    </svg>
                    <p>Share</p>
                </div>
            </div>
        </div>
        <div @click="mobile_menu = false" class="flex-grow bg-white opacity-30"></div>

    </div>
    </nav>
</template>

<script setup>
import { ref, watch } from 'vue'

const mobile_menu = ref(false);
const disableScroll = () => {
    document.body.style.overflow = "hidden";
};

const enableScroll = () => {
    document.body.style.overflow = "";
};

watch(mobile_menu, (newVal) => {
    if (newVal) {
        console.log("Dela")
        disableScroll();
    } else {
        enableScroll();
    }
});

</script>