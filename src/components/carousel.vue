<script>
export default {
    data() {
        return {
            Images: {
                imgOne: "src/assets/img/1.jpeg",
                imgTwo: "src/assets/img/2.webp",
                imgThree: "src/assets/img/3.webp",
                imgFour: "src/assets/img/4.webp",
                imgFive: "src/assets/img/5.webp",
                imgSix: "src/assets/img/6.webp",
            }
        }
    }
}
</script>


<template>
    <el-carousel :interval="2000" type="card" >
        <el-carousel-item v-for="item in Images" :key="item">
            <img :src="item"  alt="">
        </el-carousel-item>
    </el-carousel>
</template>

<style scoped>
.el-carousel {
    width: 1200px;
    height: 100%;
}
.el-carousel__item img{
    width: 1200px;
    height:100%;
    object-fit: fill;
}

.el-carousel__item h3 {
    color: #475669;
    opacity: 0.75;
    line-height: 200px;
    margin: 0;
    text-align: center;
}
</style>
