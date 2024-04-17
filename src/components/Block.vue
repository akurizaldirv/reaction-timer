<template>
    <div
        class="bg-white text-[#242424] h-screen w-full absolute z-10 top-0 text-[240px] md:text-[360px] lg:text-[480px] font-bold leading-none font-custom flex flex-row justify-center items-center cursor-pointer"
        @click="finish"
    >
        <p class="text-center">
            Click Me
        </p>
    </div>
</template>

<script>
export default {
    name: "Block",
    data() {
        return {};
    },
    props: ["isPlaying"],
    methods: {
        finish() {
            this.$emit("close");
        },
    },
};
</script>

<style scoped>
.font-custom {
    font-family: "Bebas Neue", sans-serif;
}
</style>
