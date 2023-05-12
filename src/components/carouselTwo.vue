<script>
export default {
    data() {
        return {
            addImg:"+",
            subImg:"-",
            intervalId: null, // setInterval返回的ID
            curIndex: 0,//当前序号
            isPaused: false, // 是否暂停
            pics: [{
                pid: 1,
                psrc: "src/assets/img/1.jpeg"
            }, {
                pid: 2,
                psrc: "src/assets/img/2.webp"
            }, {
                pid: 3,
                psrc: "src/assets/img/3.webp"
            }, {
                pid: 4,
                psrc: "src/assets/img/4.webp"
            }, {
                pid: 5,
                psrc: "src/assets/img/5.webp"
            }, {
                pid: 6,
                psrc: "src/assets/img/6.webp"
            }
            ]
        }
    },
    methods:{
        startInterval() {
            this.intervalId = setInterval(() => {
                console.log(this.isPaused)
                if (!this.isPaused) {
                    this.curIndex++;
                    console.log(this.curIndex)
                    if (this.curIndex == this.pics.length) {
                        this.curIndex = 0;
                    }
                }
            }, 3000);
        },
        stopInterval() {
            clearInterval(this.intervalId);
        },
        handleMouseEnter() {
            this.stopInterval()
        },
        handleMouseLeave() {
            this.isPaused = false; // 更新isPaused的值
            console.log("MouseLeave",this.isPaused)
            this.startInterval(); // 启动定时器
        },
        changeImg(vlaue){
            if (vlaue === "+"){
                this.curIndex++;
                if (this.curIndex == this.pics.length) {
                    this.curIndex = 0
                }
            }else if (vlaue === "-"){
                this.curIndex--;
                if (this.curIndex == -1) {
                    this.curIndex = this.pics.length-1
                }
            }
        }
    },
    mounted() {
        this.startInterval() // 组件挂载时启动定时器
        // setInterval(() => {
        //     this.curIndex++;
        //     if (this.curIndex == this.pics.length) {
        //         this.curIndex = 0
        //     }
        // }, 3000)
    },
}
</script>

<template>
    <transition-group tag="div" name="fade" appear="true">
        <el-icon @click="changeImg(this.subImg)" class="left"><ArrowLeft /></el-icon>
        <div class="banner"
             @mouseenter="handleMouseEnter()"
             @mouseleave="handleMouseLeave()"
        >
            <div class="bannerImg">
                <!--切换的图片-->
                <transition-group tag="div" name="fade" appear="true">
                    <img v-for="(item,index) in pics"
                         :key="item.pid" :src="item.psrc" v-show="curIndex==index" style="width: 1208px;height: 692px" />
                </transition-group>

                <!--切换的小按钮-->
                <ul class="bannerBtn">
                    <li v-for="(item,index) in pics"
                        :class="curIndex==index?'active':''"
                        @click="curIndex=index"
                        @mouseover="curIndex=index"
                        :key="item.pid">
                        <a href="javascript:void(0);" class='aBtn'>{{ index + 1 }}</a>
                    </li>
                </ul>
            </div>
        </div>
        <el-icon class="right" @click="changeImg(this.addImg)"><ArrowRight /></el-icon>
    </transition-group>
</template>


<style scoped>
.left {
    font-size: 50px;
    color: white;
    margin: auto 0;
    position: relative;
    top: 410px;
    left: -50px;
}
.right{
    font-size: 50px;
    color: white;
    margin: auto 0;
    position: relative;
    top: -379px;
    right: -1210px;
}
.fade-enter-from, .fade-leave-to{
    opacity: 0;
}
.fade-enter-to, .fade-leave-from{
    opacity: 1;
}
.fade-enter-active, .fade-leave-active{
    transition: all 3s
}
* {
    margin: 0;
    padding: 0;
}
ul li {
    list-style: none;
}

a {
    text-decoration: none;
}

.bannerImg {
    width: 1208px;
    height: 692px;
    margin: 20px auto;
    position: relative;
}

.bannerImg img {
    position: absolute;
    z-index: 800;
}

.bannerBtn {
    position: absolute;
    z-index: 1000;
    bottom: 0;
    width: 1208px;
    padding: 10px 0;
    display: flex;
    flex-direction: row;
    justify-content: center;
}

.bannerBtn li {
    width: 20px;
    height: 20px;
    background-color: #646464;
    margin: 0 5px;
    border-radius: 50%;
    font-size: 12px;
    font-family: Arial, Helvetica, sans-serif;
    line-height: 20px;
    text-align: center;
}

.bannerBtn li a {
    color: white;
}

.bannerBtn li.active {
    background-color: red;
}

</style>


