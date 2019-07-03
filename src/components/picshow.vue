/*
    @require:        elementUI

    @name:          轮播图插件
    @author:        Antilmid
    @copyright:     耕耘网络
    @description:   一个基于Vue的轮播图插件,可以快速搭建出一个最常用轮播图效果.目前没有加入其它效果,
                    后续有可能会对该项目进行扩展.
    @paramaters
    @imgUrlarr:     Array,  轮播图数组集合
    @time:          Number, 轮播图停留时间/16ms~n ms
    @height:        String, 轮播图高度
    @width:         String, 轮播图宽度
    @fit:           String, 图片显示方案  fill / contain / cover / none / scale-down  

    @event
    @gy_click:      图片被点击事件  
    
*/
<template>
    <div class="pic_div" :style="'width:'+width+'; height:'+height+';'">
        <el-image v-for="(value, i) in imgUrlarr" :key="i"
            class="images"
            :class="[active_num == i ? 'active' : '']"
            :src="value"
            :fit="fit"
            @click="inp_click(i)"
        />
        
        <!--  -->
        <div class="status_bar">
            <span v-for="(value, i) in imgUrlarr" :key="i"
                @click="set_active_num(i)"
                class="status"
                :class="[active_num == i ? 'active' : '']"
            ></span>
        </div>
    </div>
</template>

<script>
import { setInterval, clearInterval } from 'timers';
export default {
    name:"picshow",
    created(){
        this.lifetime = this.time
        this.timer = setInterval(()=>{
            this.lifetime --
            if( this.lifetime == 0 ){
                this.set_active_num(this.active_num + 1)
            }
        },1)
    },
    destroyed(){
        clearInterval(this.timer)
    },
    data() {
        return {
            lifetime:0,
            active_num:0, // 活动指针
            timer:null // 时钟句柄
        }
    },
    methods:{
        // 设置第n个图片变为激活态
        set_active_num(i){
            if(i<0){
                this.set_active_num(this.imgUrlarr.length + i)
            }else if(i > -1 && i < this.imgUrlarr.length){
                this.lifetime = this.time
                this.active_num = i
            }else{
                this.set_active_num(0 + i - this.imgUrlarr.length)
            }
        },
        inp_click(i){
            this.$emit("gy_click", [i,this])
        }
    },
    props: {
        width:{
            type: String,
            default: "100%"
        },
        height:{
            type: String,
            default: "150px"
        },
        fit:{
            type: String,
            default: "fill"
        },
        time:{
            type: Number,
            default: 300
        }, // 变换事件
        imgUrlarr: Array // 轮播图片数组
    }
}
</script>


<style scoped>
    .pic_div {
        overflow: hidden;
        display: inline-block;
        position: relative;
        background: #C0C4CC;
    }
    .images{
        position: absolute;
        left: 0;
        top: 0;
        opacity: 0;
        height: 100%;
        width: 100%;
        transition: all 1s;
    }
    .images.active{
        z-index: 10;
        opacity: 1;
    }
    .status_bar{
        top:100%;
        width: 100%;
        text-align: center;
        position: absolute;
        z-index: 11;
        margin-top: -21px;
        overflow: hidden;
    }
    .status{
        cursor: pointer;
        display: inline-block;
        height: 6px;
        width: 6px;
        margin: 0px 2.5px;
        border-radius: 100px;
        background: #fff;
        opacity: 0.4;
    }
    .status.active{
        opacity: 1;
    }
</style>

