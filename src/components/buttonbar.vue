<template>
    <!-- 样式一的按钮bar -->
    <div class="buttonbar">
        <el-row class="bt_borad" v-for="(value, i) in imgUrlarr" :key="i" :gutter="5">
            <el-col :span="24/i">
                <el-image
                    class="bt_images"
                    :src="value"
                    fit="fill"
                    @click="1"
                />
            </el-col>
        </el-row>
    </div>
</template>

<script>
    export default {
        created(){
            this.len = this.imgUrlarr.arrLen
        },
        name:"buttonbar",
        data(){
            return {
                len:0
            }
        },
        props:{
            imgUrlarr:{
                type: Array
            }
        }
    }
</script>

<style scoped>
    .buttonbar {
        position: relative;
    }
</style>
