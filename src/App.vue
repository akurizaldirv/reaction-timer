<template>
    <div class="flex flex-col items-center justify-center h-screen">
        <h1 class="text-5xl font-bold mb-3">Reaction Timer</h1>
        <div v-if="speed != null" class="flex flex-row gap-1">
            <p class="text-xl py-1 px-4">
                Your time is : {{ speed / 1000 }}s
            </p>
            <span class="rounded text-xl py-1 px-4 font-semibold" :class="color">{{ message }}</span>
        </div>
        <button
            @click="togglePlay"
            :disabled="isWaiting"
            class="border-2 text-xl border-white rounded-full py-2 px-8 hover:bg-white hover:text-black ease-in-out duration-500 mt-12"
        >
            Start
        </button>
    </div>
    <Block v-if="isPlaying" :isPlaying="isPlaying" @close="toggleFinish" />
</template>

<script>
import Block from "./components/Block.vue";

export default {
    name: "App",
    components: {
        Block,
    },
    data() {
        return {
            isPlaying: false,
            isWaiting: false,
            delayed: 0,
            timeStart: null,
            speed: null,
            color: null,
            message: null,
        };
    },
    methods: {
        togglePlay() {
            this.timeStart = null;
            this.speed = null;
            this.isWaiting = true;
            this.delayed = 2000 + Math.random() * 5000;
            setTimeout(() => {
                this.isPlaying = !this.isPlaying;
                this.timeStart = performance.now();
            }, this.delayed);
        },
        toggleFinish() {
            this.isPlaying = false;
            this.isWaiting = false;
            this.speed = performance.now() - this.timeStart;
            if (this.speed <= 100) {
                this.message = "Are you a F1 driver ?!!";
                this.color = "bg-violet-800";
            } else if (this.speed <= 300) {
                this.message = "So Fast!";
                this.color = "bg-green-700";
            } else if (this.speed <= 700) {
                this.message = "Just Normal Person";
                this.color = "bg-yellow-500";
            } else if (this.speed <= 1000) {
                this.message = "Try Again!";
                this.color = "bg-red-700";
            } else {
                this.message = "Turtle Speed";
                this.color = "bg-gray-700";
            }
            console.log(this.speed);
            console.log(this.message);
        },
    },
};
</script>
