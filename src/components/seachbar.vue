/*
    @require:        elementUI

    @name:          搜索插件
    @author:        Antilmid
    @copyright:     耕耘网络
    @description:   一个简单的搜索插件栏,基于eleUI

    @event
    @gy_focus:      聚焦事件
    @gy_blur:       失焦事件
    @gy_input:      输入事件
    @gy_bell:       小铃铛事件
    @gy_submit:     提交事件?
    
*/
<template>
    <el-row class="search_div" :gutter="10">
        <el-col :span="1" style="height:1px;"></el-col>
        <el-col class="" :span="21">
            <span class="inputbox">
                <span class="el-icon-search tipmassage"></span>
                <input type="text" name="" class="inpbox"
                    v-model="data"
                    @focus="inp_onfocus"
                    @blur="inp_onblur"
                    @input="inp_input"
                    placeholder="请输入相关商品"
                >
            </span>
        </el-col>
        <el-col class="el-icon-bell bell" :span="2" @click="inp_bell">
        </el-col>
        
        
    </el-row>
</template>

<script>
export default {
    name:"searchbar",
    data() {
        return {
            data:""
        }
    },
    methods:{
        inp_onfocus(e){
            this.$emit("gy_focus", [e,this])
        },
        inp_onblur(e){
            this.$emit("gy_blur", [e,this])
        },
        inp_input(e){
            this.$emit("gy_input", [e,this])
        },
        inp_submit(){
            this.$emit("gy_input", [this.data, this])
        },
        inp_bell(e){
            this.$emit("gy_input", [e, this])
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
    /* 整体样式 */
    .search_div {
        margin-top: 5px;
        font-size:0px; 
        text-align: center;
        position: absolute;
        top:0px;
        z-index: 11;
        width: 100%;
    }
    /* 输入框样式 */
    .inpbox {
        vertical-align: middle;
        display: inline-block;
        height: 20px;
        border: none;
        border-radius: 100px;
        outline: none;
        font-size: 14px;
        padding: 0px 30px;
        width: 100%;
        box-sizing: border-box;
    }
    .inputbox {
        width: 100%;
        position: relative;
        display: inline-block;

    }
    .tipmassage {
        color: #999;
        left: 10px;
        height: 20px;
        line-height: 20px;
        font-size: 14px;
        position: absolute;
    }
    .tip {
        margin-left: 10px;
        font-size: 14px;
    }
    /* 铃铛消息样式 */
    .bell{
        text-align: left;
        font-size: 18px;
        vertical-align: middle;
        color: #fff;
    }
</style>

