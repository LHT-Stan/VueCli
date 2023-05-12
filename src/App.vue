<script>
import Carousel from "@/components/carousel.vue";
import CarouselTwo from "@/components/carouselTwo.vue";
//增加CarouselTwo组件
export default {
    name: "App",
    components: {
        Carousel,
        CarouselTwo
    }
};
</script>

<template>
<!--    <carousel></carousel>-->
    <carousel-two></carousel-two>
</template>

<style scoped>

</style>
